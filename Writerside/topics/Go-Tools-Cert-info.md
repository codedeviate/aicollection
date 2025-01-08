# Cert info

This article explains how to create a Go program that connects to a web server, extracts SSL certificate information, and displays key details such as the certificate's expiration date, issuer, and certificate chain. We will organize the code into reusable modules for clarity and maintainability.

---

### Step 1: Overview of the Program
The program connects to a given HTTPS endpoint, retrieves the server's SSL certificate, and parses the details. The extracted information includes:
- **Certificate Expiry Date**
- **Certificate Issuer**
- **Certificate Chain**

---

### Step 2: Code Organization
We will divide the program into the following modules:
1. **`main.go`**: The entry point of the application.
2. **`certificate/certificate.go`**: Handles the extraction and parsing of SSL certificates.
3. **`utils/utils.go`**: Provides utility functions for data formatting.

---

### Step 3: The Code

#### 1. `main.go`
This is the entry point of the program. It accepts a domain as input, fetches certificate information, and displays the results.

```go
package main

import (
	"fmt"
	"log"
	"os"

	"github.com/username/certinfo/certificate"
)

func main() {
	if len(os.Args) < 2 {
		log.Fatalf("Usage: %s <hostname>", os.Args[0])
	}

	hostname := os.Args[1]
	certInfo, err := certificate.FetchCertificateInfo(hostname)
	if err != nil {
		log.Fatalf("Error fetching certificate: %v", err)
	}

	fmt.Printf("Certificate Information for %s:\n", hostname)
	fmt.Printf("Issuer: %s\n", certInfo.Issuer)
	fmt.Printf("Expiry Date: %s\n", certInfo.ExpiryDate)
	fmt.Println("Certificate Chain:")
	for i, chainCert := range certInfo.Chain {
		fmt.Printf("  [%d] %s\n", i+1, chainCert.Subject)
	}
}

```

---

#### 2. `certificate/certificate.go`
This module contains logic to retrieve and parse SSL certificates.

```go
package certificate

import (
	"crypto/tls"
	"crypto/x509"
	"fmt"
	"time"
)

// CertInfo holds key certificate details.
type CertInfo struct {
	Issuer     string
	ExpiryDate string
	Chain      []*x509.Certificate
}

// FetchCertificateInfo connects to a host and extracts SSL certificate details.
func FetchCertificateInfo(hostname string) (*CertInfo, error) {
	conn, err := tls.Dial("tcp", fmt.Sprintf("%s:443", hostname), nil)
	if err != nil {
		return nil, fmt.Errorf("failed to connect to %s: %w", hostname, err)
	}
	defer conn.Close()

	certs := conn.ConnectionState().PeerCertificates
	if len(certs) == 0 {
		return nil, fmt.Errorf("no certificates found for %s", hostname)
	}

	// Extract main certificate details
	mainCert := certs[0]
	issuer := mainCert.Issuer.String()
	expiryDate := mainCert.NotAfter.Format(time.RFC1123)

	// Return all certificates in the chain
	return &CertInfo{
		Issuer:     issuer,
		ExpiryDate: expiryDate,
		Chain:      certs,
	}, nil
}

```

---

#### 3. `utils/utils.go`
This module can contains utility functions for formatting certificate data. For now, we will keep it minimal.

```go
package utils

// No utility functions for this example, but you could add functions
// like chain formatting or date comparison here.

```

---

### Step 4: Running the Program

1. **Build and Run**: Save the files in the appropriate directories and build the program using `go build`.
2. **Run with Hostname**:
   ```bash
   ./sslinfo example.com
   ```

3. **Output Example**:
   ```
   Certificate Information for example.com:
   Issuer: C=US, O=Let's Encrypt, CN=R3
   Expiry Date: Sun, 30 Jan 2025 15:04:05 UTC
   Certificate Chain:
     [1] CN=example.com
     [2] CN=R3
     [3] CN=ISRG Root X1
   ```

---

### Step 5: Explanation of Key Concepts

#### 1. **TLS Dialing**:
The `tls.Dial` function establishes a secure connection to the server and retrieves the certificate chain. This approach ensures we work with live certificate data.

#### 2. **Parsing Certificates**:
The `PeerCertificates` field from the connection state provides the full certificate chain. This allows us to display not only the leaf certificate but also intermediate and root certificates.

#### 3. **Time Formatting**:
The `time.RFC1123` format ensures human-readable dates are displayed.

---

### Step 6: Possible Enhancements
- **Add Command-Line Flags**: Support for flags like `--verbose` for detailed output.
- **Verify Certificates**: Validate certificates against system trust stores.
- **Error Handling**: Improve error reporting for common issues like expired certificates.

---

With this modular approach, you can easily extend or maintain the code as needed. The program is simple yet powerful, allowing you to inspect SSL certificates with ease.