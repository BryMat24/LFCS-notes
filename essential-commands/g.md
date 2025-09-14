# 📑 OpenSSL Certificates Cheat Sheet

---

## 1. 🔑 Generate Private Keys

### RSA Private Key

```bash
openssl genrsa -out private.key 2048
```

## 2. 📜 Create a Certificate Signing Request (CSR)

```
openssl req -new -key private.key -out request.csr
openssl req -text -noout -verify -in request.csr # view CSR content
```

## 3. 📝 Generate a Self-Signed Certificate

```
openssl req -x509 -new -nodes -key private.key -sha256 -days 365 -out certificate.crt
openssl x509 -in certificate.crt -text -noout # see detail
```
