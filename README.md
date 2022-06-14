# A Simple Insecure Certificate Manager

A very simple setup to generate certificates for your local environment.

## Pre-requisites

- Task (https://taskfile.dev/installation/)
- OpenSSL 1.1.1 or newer - use your platform's package manager, windows -> [Chocolatey package](https://community.chocolatey.org/packages/openssl)
- GNU CoreUtils (For Windows) [Chocolatey package](https://community.chocolatey.org/packages/gnuwin32-coreutils.portable)

## Configuration

Open ca.env and modify it to suit your needs;

## Directory Layout

### root

Contains Root CA configuration and related resources. `certs/ca.cert.pem` file contains the Root CA's certificate,
which can be used to trust any issued certiticates through this script.

### intermediate

Contains Intermediate CA configuration and related resources. `certs/intermediate.cert.pem` file contains the Intermediate CA's certificate,
and `certs/ca-chain.pem` both Root and Intermediate CA certificates.

## Tasks

### Generate a Server Certificate

To generate a server certificate with subject alternative name field set as DNS:my.example.com;

```shell
task server-cert HOSTNAME=my.example.com
```

will generate a key pair and also certificates for `my.example.com`. The generated files are;

- `intermediate/private/my.example.com.key.pem` is the generated private key (no password set)
- `intermediate/certs/my.example.com.cert.pem` is the generated server certificate
- `intermediate/pkcs/my.example.com.pfx` is the PKCS12 file that contains both the private key and certificate (password is `changeit`)

