# Docker-Nginx-Certbot

Docker boilerplate for Nginx + Certbot on non-interactive systems

---

# Usage

## Docker Environment

### Required

- `DOMAIN`: The domain to generate the certificates.
- `CERTBOT_EMAIL`: Your e-mail address. Used by Let's Encrypt to contact you in case of security issues.

### Optional

- `STAGING`: Set to `1` to use Let's Encrypt's staging servers (default: `0`)
- `RENEWAL_INTERVAL`: Time interval between certbot's renewal checks (default: `12h`)
- `RSA_KEY_SIZE`: The size of the RSA encryption keys (default: `2048`)
- `USE_ECDSA`: Set to `0` to have certbot use RSA instead of ECDSA (default: `1`)
- `ELLIPTIC_CURVE`: The size/curve of the ECDSA keys (default: `secp256r1`)

### Advanced

- `DEBUG`: Set to `1` to enable debug messages and use the [`nginx-debug`][10] binary (default: `0`)

# Acknowledgments

This repository is heavily based on [`@JonasAlfredsson`][1]'s work. If you like this version you should also leave a star on his repo.

[1]: https://github.com/JonasAlfredsson/docker-nginx-certbot
