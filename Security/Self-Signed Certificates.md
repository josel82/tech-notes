## Documentation
[How to create a valid self signed SSL Certificate](https://www.youtube.com/watch?v=VH4gXcvkmOY&t=1303s)
[CristianLempa/cheat-sheets/misc/ssl-certs.md](https://github.com/ChristianLempa/cheat-sheets/blob/main/misc/ssl-certs.md)

## Procedure
This is how we can generate our own Self-Signed Certificates
1. We need a Certificate Autority (CA) that issues our certificate. We start by generating a private key for the CA. This process will require a passphrase that needs to be kept in a save place. You will need this key to generate certificates.
```bash
openssl genrsa -aes256 -out ca-key.pem 4096
```

2. Next, we generate a CA certificate which corresponds to the private key above. This CA certificate will be valid for 10 years.
```bash
openssl req -new -x509 -sha256 -days 3650 -key ca-key.pem -out ca.pem
```

You can check the newly created CA certificate by running the following command:
```bash
openssl x509 -in ca.pem -text
```

3. Now we can proceed to generating our self-signed certificates. We will start by generating a RSA key:
```bash
openssl genrsa -out cert-key.pem 4096
```

4. Then we generate a certificate sign request. (This certificate needs to be signed by the CA). 
```bash
openssl req -new -sha256 -subj "/CN=yourcn" -key cert-key.pem -out cert.csr
```

5. Next up, we generate a config file where we'll specify the domains / IP addresses the certificate will be valid for.
```bash
echo "subjectAltName=DNS:*.mydomain.home,IP:10.0.0.150" >> extfile.cnf
```

6. Generate the certificate from the Certificate Sign Request.
```bash
openssl x509 -req -sha256 -days 3650 -in cert.csr -CA ca.pem -CAkey ca-key.pem -out cert.pem -extfile extfile.cnf -CAcreateserial 
```

7. Now we need to conbine bothe the CA certificate and the certificate to create a certificate chain.
```bash
cat cert.pem > fullchain.pem
cat ca.pem >> fullchain.pem
```

8. Once all this is done, we can then import our self-signed CA to our system. Which is done differently for every OS. In macos you just need to open the Keychain Access App and drag and drop `ca.pem` into either the "login" or "system" keychain. [source](https://support.apple.com/en-gb/guide/keychain-access/kyca2431/mac)
9. Lasty you need to import your certificate into your different web UIs. When you do this remember that 


## Publick Key
Here is how you can generate a public key from the private key
```bash
openssl rsa -in cert-key.pem -pubout -out publickey.crt
```

RSAPubKey Format
```bash
openssl rsa -in cert-key.pem -RSAPublicKey_out -out cert-pubkey.pem
```
