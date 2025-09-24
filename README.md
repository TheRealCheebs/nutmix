_Disclaimer: The author is NOT a cryptographer and this work has not been reviewed. This means that there is very likely
a fatal flaw somewhere. Cashu is still experimental and not production-ready._

_Don't be reckless:_ This project is in early development; it does, however, work with real sats! Always use amounts you
don't mind losing.

_This project is in active development; it has not gone through optimization and refactoring yet_.

# Nutmix

Nutmix is an alternative Cashu mint written in Go, designed for ease of use, feature completeness, and minimal complexity.

Please test in Mutinynet at: *https://mutinynet.nutmix.cash*

## Objective

Nutmix provides a built-in dashboard for administration and log management, making it easy to operate and monitor the mint.

---

### Run the Mint

You can run this project locally or in a Docker container.

Most of the setup process is handled in the **Admin Dashboard**, but you’ll need to configure a few things first.
Start by creating an `.env` file (use the provided `env.example` as a reference).

#### Required Environment Variables

1. **Database**
   - Set a strong `POSTGRES_PASSWORD`.
   - Ensure the username and password match the values in your `DATABASE_URL`.

2. **Private Key**
   - Add a private key via the `MINT_PRIVATE_KEY` environment variable, **or** configure a connection to a remote signer.

3. **Admin Access**
   - Add your npub to the `ADMIN_NOSTR_NPUB` environment variable so you can log in to the Admin Dashboard and finish setup.

---

⚠️ The mint will stop and print out errors if these items are not configured properly.

---

### Running with Docker

To run the included Docker Compose setup (using Traefik), you’ll need to set the variables under **HOSTING** in your `.env` file for your domains.

Once configured, starting Nutmix is as simple as running:

```bash
docker compose up -d
```

## Setting up a remote signer.

Nutmix supports connecting to a remote signer. Currently, there are two implementations:

- [Nutvault](https://github.com/lescuer97/nutvault)
- [cdk-signatory](https://github.com/cashubtc/cdk/tree/main/crates/cdk-signatory)

To use a remote signer:

1. Set the `SIGNER_TYPE` environment variable to either `abstract_socket` or `network`.
   - If you choose `network`, you’ll also need to set `NETWORK_SIGNER_ADDRESS`.

2. Configure mTLS so the mint can securely communicate with the signer. Add the following environment variables with the correct file paths:

```bash
SIGNER_CLIENT_TLS_KEY=<path-to-key>
SIGNER_CLIENT_TLS_CERT=<path-to-cert>
SIGNER_CA_CERT=<path-to-ca-cert>
```

## Video Walkthrough
#### Video on .env setup
[![Video on .env setup](https://cdn.hzrd149.com/0930b6e46cfe03a70345930d55b2eff51b0eb39d6e6eb4305b42b7736398f49c.png)](https://cdn.hzrd149.com/0ef3cb33401dbdd002039d01c0f749491c26720a80b23b885ae0f569ebd9f7b3.mp4)

#### Setup Lightning node
[![Setup Lightning node](https://cdn.hzrd149.com/c2175c7a310026f0450f98146f9dd180979909aaa464aa4376a75eb25b013b10.png)](https://cdn.hzrd149.com/905025ea49d48e36890f87ab05a7be75b141331e25ec8a326a29adfc9cb4cd0a.mp4)

#### Walkthrough of dashboard
[![Walkthrough of dashboard](https://cdn.hzrd149.com/9f967999398e74ffb5ae079bb7e06b58ef8470204b05a21647c5b4e18c71c8d9.png)](https://cdn.hzrd149.com/72a5a65e027370084d45586084098f97ae3631f86bad932656b5c9532be7ba93.mp4)


## Supported NUTs
[NUTs REPO](https://github.com/cashubtc/nuts/):

- [x] [NUT-00](https://github.com/cashubtc/nuts/blob/main/00.md) - Cryptography and Models
- [x] [NUT-01](https://github.com/cashubtc/nuts/blob/main/01.md) - Mint public keys
- [x] [NUT-02](https://github.com/cashubtc/nuts/blob/main/02.md) - Keysets and fees
- [x] [NUT-03](https://github.com/cashubtc/nuts/blob/main/03.md) - Swapping tokens
- [x] [NUT-04](https://github.com/cashubtc/nuts/blob/main/04.md) - Minting tokens
- [x] [NUT-05](https://github.com/cashubtc/nuts/blob/main/05.md) - Melting tokens
- [x] [NUT-06](https://github.com/cashubtc/nuts/blob/main/06.md) - Mint info
- [x] [NUT-07](https://github.com/cashubtc/nuts/blob/main/07.md) - Token state check
- [x] [NUT-08](https://github.com/cashubtc/nuts/blob/main/08.md) - Overpaid Lightning fees
- [x] [NUT-09](https://github.com/cashubtc/nuts/blob/main/09.md) - Signature restore
- [x] [NUT-10](https://github.com/cashubtc/nuts/blob/main/10.md) - Spending conditions
- [x] [NUT-11](https://github.com/cashubtc/nuts/blob/main/11.md) - Pay-To-Pubkey (P2PK)
- [x] [NUT-12](https://github.com/cashubtc/nuts/blob/main/12.md) - DLEQ proofs
- [x] [NUT-14](https://github.com/cashubtc/nuts/blob/main/14.md) - Hashed Timelock Contracts (HTLCs)
- [x] [NUT-15](https://github.com/cashubtc/nuts/blob/main/15.md) - Partial multi-path payments (MPP)
- [x] [NUT-17](https://github.com/cashubtc/nuts/blob/main/17.md) - WebSocket subscriptions
- [x] [NUT-19](https://github.com/cashubtc/nuts/blob/main/19.md) - Cached Responses
- [x] [NUT-20](https://github.com/cashubtc/nuts/blob/main/20.md) - Signature on Mint Quote
- [x] [NUT-21](https://github.com/cashubtc/nuts/blob/main/21.md) - Clear authentication
- [x] [NUT-22](https://github.com/cashubtc/nuts/blob/main/22.md) - Blind authentication

Non official NUT:
- [x] [NUT-XX](https://github.com/cashubtc/nuts/blob/main/22.md)


## Development

For detailed development setup instructions, see [Development.md](docs/DEVELOPMENT.md)

### Quick Start


Choose the setup that best fits your needs:

#### Option 1: Full Docker Compose (Complete Stack)
```bash
# Clone the repository
git clone https://github.com/yourusername/nutmix.git
cd nutmix

# Start all services (traefik, postgres, app)
just docker-up
```
This option runs the entire stack in Docker containers, including:
  - Traefik (reverse proxy)
  - PostgreSQL database
  - Nutmix application

#### Option 2: Development Setup (Database in Docker, App Locally)
```bash
# Clone the repository
git clone https://github.com/lescuer97/nutmix.git
cd nutmix

# Install dependencies and start the development environment
just deps
just dev
```

This option is recommended for active development:
  - PostgreSQL runs in Docker
  - Application runs locally on your machine
  - Automatically installs dependencies on first run
  - Enables faster development iterations

### Keycloak Notice

Keycloak-related configuration and environment variables are present in some files, but Keycloak is not currently used or integrated in this project.

## Support

Pull requests, issues, and suggestions are always welcome — the more eyes on the project, the better.

If you’d like to support development financially, donations are greatly appreciated. Contributions help fund ongoing development of the mint and testing servers.


*on-chain silent payments*

```
sp1qq0fju879lh2rgvwjjd7e78pg4gnr7a8aumth8qlezdgjs2rwzk7ssq5jm7v27cuuk5dyjfurdy8t8jflkcx0sluwez350kjjd45y7nnx3vgmjqjq
```

*Donate with lightning*

[nutmix@npub.cash](https://npub.cash/pay/nutmix)


*Donate with on-chain*

```
bc1qp7lswgftpgrkt00vszrm63dmkq3nuxjv60czk6
```

*Donate with Monero*

```
84yCRZY6BXebs8xWE6Yzj6S6cE17uLhkTSynneVPmejjWAcgBtnV7UEUiZqJNLE4pXaPmXNkJuhcAYbpu49zAdVsEZqqxac
```
