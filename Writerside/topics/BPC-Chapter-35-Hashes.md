# Chapter 35 - Hashes

Hashes are a fundamental concept in computer science and cryptography. They are used in a wide variety of applications, from data integrity checks to password storage and digital signatures. A hash function takes an input (or message) and produces a fixed-size string of bytes, typically a hexadecimal number, that is unique to the input. This output is called a hash value, hash code, or simply a hash.

In this article, we will delve into the basics of hash functions, their properties, and common algorithms like MD4, MD5, SHA1, SHA256, SHA512, CRC32, and CRC64. We will also discuss practical applications and examples in multiple programming languages.

---

## What Are Hash Functions?

A hash function is a mathematical algorithm that maps data of arbitrary size to a fixed size. Hash functions are deterministic, meaning the same input will always produce the same output. However, small changes to the input produce completely different outputs, making hashes highly sensitive to input changes.

### Properties of Good Hash Functions

1. **Deterministic**: The same input always results in the same hash.
2. **Fast Computation**: The function should be quick to compute the hash value.
3. **Pre-image Resistance**: It should be computationally infeasible to reverse the hash and retrieve the original input.
4. **Collision Resistance**: Different inputs should not produce the same hash value.
5. **Avalanche Effect**: A small change in the input results in a significantly different hash.

---

## Common Hash Algorithms and Their Characteristics

### MD4

MD4 (Message Digest Algorithm 4) was designed by Ronald Rivest in 1990. It is a cryptographic hash function producing a 128-bit hash value. MD4 is fast but considered insecure due to vulnerabilities to cryptographic attacks.

**Usage**: Primarily of historical interest; rarely used today.

### MD5

MD5 (Message Digest Algorithm 5), also by Ronald Rivest, generates a 128-bit hash. It was widely used in the past for checksums and password storage but is no longer secure against cryptographic attacks like collision and pre-image attacks.

**Usage**: Legacy systems, data integrity (non-critical).

### SHA1

SHA1 (Secure Hash Algorithm 1) produces a 160-bit hash and was widely used for digital signatures and certificates. However, it has been deprecated due to vulnerabilities to collision attacks.

**Usage**: Legacy systems, deprecated in security-sensitive contexts.

### SHA256

SHA256, part of the SHA-2 family, produces a 256-bit hash and is significantly more secure than SHA1. It is widely used for password hashing, digital certificates, and blockchain.

**Usage**: Password hashing, digital signatures, blockchain.

### SHA512

SHA512 is another member of the SHA-2 family, producing a 512-bit hash. It offers greater security but is slower than SHA256, making it suitable for scenarios requiring higher computational resistance.

**Usage**: Cryptography, secure communications.

### CRC32

CRC32 (Cyclic Redundancy Check 32-bit) is not a cryptographic hash but a checksum used to detect accidental changes in data. It is fast and commonly used for file integrity checks and network error detection.

**Usage**: File integrity checks, error detection.

### CRC64

CRC64 is an extended version of CRC32 that produces a 64-bit checksum. It provides better collision resistance for larger datasets and is used in specific scenarios like databases and distributed systems.

**Usage**: File systems, large-scale data integrity checks.

---

## Applications of Hash Functions

### Password Storage

Hashes are used to store passwords securely. Instead of storing passwords in plain text, applications store their hashes. Combined with techniques like salting, this approach ensures that even if a database is compromised, the original passwords are not easily retrievable.

### Data Integrity Verification

Hashes are used to verify the integrity of files and data. By comparing the hash of a downloaded file with a known hash, users can ensure the file has not been tampered with.

### Digital Signatures

Digital signatures use hash functions to verify the authenticity and integrity of messages or documents. A hash of the content is encrypted with the sender's private key, and the recipient can decrypt it with the sender's public key to verify the content.

### Blockchain

In blockchain technology, hashes are used to link blocks together and ensure data integrity. Each block contains a hash of the previous block, forming a secure chain.

### Error Detection

CRC32 and CRC64 are widely used for detecting errors in data transmission and storage. They ensure that accidental changes can be identified and corrected.

---

## Implementing Hash Functions in Code

Here are examples of how to use these hash functions in Python, PHP, Go, C++, and Zig.

### Python Example

```python
import hashlib
import zlib

# MD5
md5_hash = hashlib.md5(b"Hello, World!").hexdigest()
print("MD5:", md5_hash)

# SHA256
sha256_hash = hashlib.sha256(b"Hello, World!").hexdigest()
print("SHA256:", sha256_hash)

# CRC32
crc32_hash = zlib.crc32(b"Hello, World!")
print("CRC32:", crc32_hash)
```

### PHP Example

```php
<?php
// MD5
echo "MD5: " . md5("Hello, World!") . PHP_EOL;

// SHA256
echo "SHA256: " . hash('sha256', "Hello, World!") . PHP_EOL;

// CRC32
echo "CRC32: " . hash('crc32', "Hello, World!") . PHP_EOL;
?>
```

### Go Example

```go
package main

import (
	"crypto/md5"
	"crypto/sha256"
	"fmt"
	"hash/crc32"
)

func main() {
	// MD5
	md5Hash := md5.Sum([]byte("Hello, World!"))
	fmt.Printf("MD5: %x\n", md5Hash)

	// SHA256
	sha256Hash := sha256.Sum256([]byte("Hello, World!"))
	fmt.Printf("SHA256: %x\n", sha256Hash)

	// CRC32
	crc32Hash := crc32.ChecksumIEEE([]byte("Hello, World!"))
	fmt.Printf("CRC32: %x\n", crc32Hash)
}
```

### C++ Example

```cpp
#include <iostream>
#include <openssl/md5.h>
#include <openssl/sha.h>
#include <zlib.h>

void print_hash(const unsigned char* hash, size_t length) {
    for (size_t i = 0; i < length; ++i) {
        printf("%02x", hash[i]);
    }
    std::cout << std::endl;
}

int main() {
    const char* input = "Hello, World!";
    
    // MD5
    unsigned char md5_hash[MD5_DIGEST_LENGTH];
    MD5((unsigned char*)input, strlen(input), md5_hash);
    std::cout << "MD5: ";
    print_hash(md5_hash, MD5_DIGEST_LENGTH);

    // SHA256
    unsigned char sha256_hash[SHA256_DIGEST_LENGTH];
    SHA256((unsigned char*)input, strlen(input), sha256_hash);
    std::cout << "SHA256: ";
    print_hash(sha256_hash, SHA256_DIGEST_LENGTH);

    // CRC32
    uint32_t crc32_hash = crc32(0, (unsigned char*)input, strlen(input));
    std::cout << "CRC32: " << std::hex << crc32_hash << std::endl;

    return 0;
}
```

### Zig Example

```zig
const std = @import("std");

pub fn main() !void {
    const input = "Hello, World!";

    // MD5
    const md5 = try std.crypto.md5Hasher();
    md5.update(input);
    const md5_hash = md5.final();
    std.debug.print("MD5: {x}\n", .{md5_hash});

    // SHA256
    const sha256 = try std.crypto.sha256Hasher();
    sha256.update(input);
    const sha256_hash = sha256.final();
    std.debug.print("SHA256: {x}\n", .{sha256_hash});

    // CRC32
    const crc32 = std.hash.crc32(input);
    std.debug.print("CRC32: {x}\n", .{crc32});
}
```

---

## Conclusion

Hash functions are a versatile tool in modern computing, serving a variety of purposes from securing passwords to ensuring data integrity. While algorithms like MD5 and SHA1 are considered outdated, others like SHA256 and SHA512 continue to be robust for cryptographic purposes. CRC32 and CRC64 remain valuable for error detection in non-cryptographic contexts. Understanding and implementing these algorithms can enhance the security and reliability of applications.