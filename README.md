# Docker-Nginx-Certbot

Generating TLS certificates through [`Certbot`][1] for a dockerized web application can be tricky and require manual configurations, specially on a host machine without terminal access (e.g. AWS Elastic Beanstalk).

One could setup a load balancer (e.g. AWS ELB) that deals with the TLS certificates, but for single instance systems that may be an overkill/expensive solution.

This project aims to remove the complexity of this task by deploying a Docker container that will manage creation and renewal of TLS certificates automatically.

# Usage

This is a boilerplate, therefore it needs to be integrated into your project. The files and folders of this project have the `-dnc` suffix so it's harder to overwrite any of your files by accident.

## Before you start

- This guide expects you to already own a domain which points at the correct IP address, and that you have both port 80 and 443 correctly forwarded if you are behind NAT.

- The `docker-compose-dnc.yml` example file has the necessary structure to build the project correctly. You can just port the necessary parts to your own docker-compose file or just update it with your api service.

- The `nginx-certbot` service should be able to reach the api service, usually thats achieved by placing both services on the same Docker network.

When you're happy with you configuration just run:

```
docker-compose -f <your-final-docker-compose.yml> up
```

---

## Docker Environment

### Required

- `DOMAIN`: The domain that will receive the certificate.
- `CERTBOT_EMAIL`: Your e-mail address. Used by Let's Encrypt to contact you in case of security issues.

### Optional

- `API_DOCKER_SERVICE`: Docker service name for your API. Used to configure reverse proxy. (default: `production-api`)
- `API_DOCKER_PORT`: Docker container port for your API. Used to configure reverse proxy. (default: `8080`)
- `STAGING`: Set to `1` to use Let's Encrypt's staging servers (default: `0`)
- `FORCE_RENEWAL`: Set to `1` to force Certbot to renew the certificate, even if it isn't expired. [Beware of rate limits] (default: `0`)
- `RENEWAL_INTERVAL`: Time interval between Certbot's renewal checks (default: `12h`)
- `RSA_KEY_SIZE`: The size of the RSA encryption keys (default: `2048`)
- `USE_ECDSA`: Set to `0` to have certbot use RSA instead of ECDSA (default: `1`)
- `ELLIPTIC_CURVE`: The size/curve of the ECDSA keys (default: `secp256r1`)

### Advanced

- `DEBUG`: Set to `1` to enable debug messages and use the `nginx-debug` binary (default: `0`)

# Acknowledgments

This repository is heavily based on [`@JonasAlfredsson`][2]'s work. If you like this version you should also leave a star on his repo.

[1]: https://certbot.eff.org
[2]: https://github.com/JonasAlfredsson/docker-nginx-certbot
