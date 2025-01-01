# Create certificate via Let&apos;s Encrypt

To create a certificate through **Let's Encrypt**, a free and automated Certificate Authority (CA), follow these steps. Let's Encrypt provides SSL/TLS certificates for securing websites and supports automation through tools like **Certbot**.

---

## Step 1: Prerequisites
1. **Domain Name**: Ensure you have a registered domain name (e.g., `example.com`) pointing to your server's IP address.
2. **Server**: You need a web server (e.g., Apache, Nginx) running on a server with a public IP address.
3. **Root Access**: Access to the server with sudo or root privileges.
4. **Port 80 Open**: Ensure HTTP (port 80) is open for Let's Encrypt to perform domain validation.

---

## Step 2: Install Certbot
Certbot is the official Let's Encrypt client that automates the process of obtaining and renewing certificates.

### On Debian/Ubuntu:
```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx  # For Nginx
# OR
sudo apt install certbot python3-certbot-apache # For Apache
```

### On CentOS/RHEL:
```bash
sudo yum install epel-release
sudo yum install certbot python3-certbot-nginx  # For Nginx
# OR
sudo yum install certbot python3-certbot-apache # For Apache
```

---

## Step 3: Obtain a Certificate
You can obtain a certificate automatically or manually, depending on your setup.

### Automatic Certificate Installation
For supported web servers like Apache or Nginx, Certbot can configure the server automatically.

#### Example for Nginx:
```bash
sudo certbot --nginx
```

#### Example for Apache:
```bash
sudo certbot --apache
```

Certbot will:
1. Detect your web server configuration.
2. Prompt you to choose a domain name from the list of virtual hosts.
3. Obtain and install the certificate automatically.

---

### Manual Certificate Installation
If your web server is custom or unsupported, use the standalone method.

#### Command:
```bash
sudo certbot certonly --standalone -d example.com -d www.example.com
```

- `certonly`: Obtain the certificate without modifying the server configuration.
- `--standalone`: Certbot will run its temporary web server for validation.
- `-d`: Specify domain names for the certificate.

The certificate files will be saved to `/etc/letsencrypt/live/example.com/`.

---

## Step 4: Test Your Certificate
Verify that the certificate is working by accessing your website via HTTPS:
```bash
https://example.com
```

You can also test your certificate using SSL Labs:
[SSL Labs Test](https://www.ssllabs.com/ssltest/)

---

## Step 5: Automate Renewal
Let's Encrypt certificates are valid for 90 days. Certbot sets up automatic renewal by default via a systemd timer.

To check the timer:
```bash
sudo systemctl list-timers | grep certbot
```

You can test renewal manually:
```bash
sudo certbot renew --dry-run
```

---

## Step 6: Common Commands
- **List Certificates**:
  ```bash
  sudo certbot certificates
  ```

- **Revoke a Certificate**:
  ```bash
  sudo certbot revoke --cert-path /etc/letsencrypt/live/example.com/cert.pem
  ```

- **Delete a Certificate**:
  ```bash
  sudo certbot delete --cert-name example.com
  ```

---

## Example Scenarios

### Example 1: Single Domain with Nginx
```bash
sudo certbot --nginx -d example.com
```

### Example 2: Multiple Subdomains
```bash
sudo certbot --nginx -d example.com -d www.example.com -d blog.example.com
```

### Example 3: Standalone with Wildcard Domain
Wildcard certificates require DNS validation:
```bash
sudo certbot certonly --manual -d *.example.com --preferred-challenges dns
```
You will need to add a DNS TXT record for `_acme-challenge.example.com` as instructed during the process.

---

## Troubleshooting
1. **Port 80 Blocked**: Ensure no firewall or ISP restrictions on HTTP.
   ```bash
   sudo ufw allow 80
   sudo ufw allow 443
   ```
2. **Certificate Not Loading**: Check web server configuration for HTTPS and restart the service:
   ```bash
   sudo systemctl restart nginx
   ```
3. **Domain Validation Errors**: Ensure the domain's DNS records are correctly pointing to the server.

---

## Additional Resources
- Let's Encrypt Documentation: [https://letsencrypt.org/docs/](https://letsencrypt.org/docs/)
- Certbot Website: [https://certbot.eff.org/](https://certbot.eff.org/)

By following these steps, you can easily obtain and manage Let's Encrypt certificates for your website.