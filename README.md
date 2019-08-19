# Generate private key

```
openssl genrsa -out private_key.pem 2048
```

# Generate public key from the private one

```
openssl rsa -in private_key.pem -outform PEM -pubout -out public_key.pem
```

# Encrypting a message

```
echo 'This is a secret message, for authorized parties only' > secret.txt
openssl rsautl -encrypt -pubin -inkey public_key.pem -in secret.txt -out secret.enc
```

# Decrypting a message

```
openssl rsautl -decrypt -inkey private_key.pem -in secret.enc
```

# Creating a hash digest

## To create a hash digest

```
openssl dgst -sha256 -sign private_key.pem -out secret.txt.sha256 secret.txt
```

## Verify that the file hasn't been tampered by using the hash digest

```
openssl dgst -sha256 -verify public_key.pem -signature secret.txt.sha256 secret.txt
```
