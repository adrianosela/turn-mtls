# mtls-turn

This directory contains an end-to-end example of how to use client TLS certificates for authentication of TURN clients. To be precise, the example demonstrates mutual TLS (mTLS) where both the client and server ensure each other present a TLS certificate signed by the same trusted Certificate Authority (CA).

**Authentication Model:** Unlike other examples that use a static list of username/password pairs, this example uses certificate-based authentication. The server trusts any client with a certificate signed by the trusted CA. Normally, the username:password combination is used for message integrity, but this is unnecessary here because TLS itself provides integrity and authentication through the certificate validation.

> In this example, the AuthHandler derives the auth key from the certificate's CommonName (treating it as the username) and an empty string as the password. Note that it doesn't matter which part of the certificate is used to derive the auth key (CommonName, serial number, SANs, etc.), or even if no part of the certificate is used, as long as the client and server agree on the scheme and arrive at the same value.

To run the example:

1) Generate demo certificates (CA, server, and client certificates)

```
make generate-certs
```

2) Run the TURN server

```
make run-server
```

3) Run the TURN client

```
make run-client
```
