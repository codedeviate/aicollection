# OpenSSL

{is-library="true"}


<snippet id="CreateSelfSignedCert">

You need SSL certificates to run this server. You can generate self-signed certificates using OpenSSL:

```sh
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes -subj "/C=SE/ST=Skåne/L=Malmö/O=Example/OU=Development/CN=example.com"
```

> Self-signed certificates may cause problems in web browsers due to security warnings. For production use, consider obtaining certificates from a trusted Certificate Authority (CA).
>
> To allow self-signed certificates in `curl`, use the `-k` or `--insecure` option, in `wget` use `--no-check-certificate`, and in browsers, proceed with the security exception.

</snippet>