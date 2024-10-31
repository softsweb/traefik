# Traefik Setup with Docker Compose for Reverse Proxy and HTTPS

This project demonstrates how to configure Traefik using Docker to manage web traffic, set up reverse proxies, and enable HTTPS for applications.

### By the end of this tutorial, you’ll be able to:

- Deploy Traefik with Docker Compose.
- Configure Traefik as a reverse proxy for your Docker services.
- Set up HTTPS with automatic Let's Encrypt SSL certificates.


## Prerequisites

To follow along, make sure you have:

- A server or VM (preferably with Linux) with a public IP address.
- Docker Engine installed.
- A domain name pointing to your server.
For this tutorial, we used an Azure Virtual Machine with the domain dev.softsweb.site.

## Setup Guide

1. Directory Setup

Navigate to the /opt directory, create a directory for Traefik, and change to it.

```
cd /opt
mkdir traefik
cd traefik
```

2. Docker Compose Configuration

Create a docker-compose.yml file with the content from [traefik/docker-compose.yml](traefik/docker-compose.yml)

### Explanation of Key Sections:

Command Options:

- providers.docker: Automatically discovers Docker services.
- providers.file.directory: Specifies a configuration directory.
- api.insecure: Enables the Traefik dashboard for monitoring.
- certificatesResolvers: Configures Let's Encrypt certificates.

Ports:
- 80 and 443: HTTP and HTTPS traffic.
- 8080: Dashboard access (disabled in production for security).

3. Additional Traefik Configurations

Create the configuration directory and a [/etc/traefik/traefik.yml](/etc/traefik/traefik.yml) file within it.

```
mkdir -p /etc/traefik/certs
nano /etc/traefik/traefik.yml
```

4. Network Creation and Starting Traefik

Create a Docker network and launch Traefik.

```
docker network create traefik
docker-compose up -d
```

5. Configuring an Example Service

Let’s set up an NGINX container with (docker-compose)[/nginx/docker-compose.yml] as an example service to be managed by Traefik.

6. Testing the Setup
Navigate to https://yourdomain.com You should see the default NGINX page, indicating that Traefik is properly routing traffic and applying HTTPS.

## Additional Configuration Options
For further customization, you can adjust middleware settings such as CORS headers and rate limits in `traefik.yml`.

## Troubleshooting
If something doesn’t work as expected:

1. Verify domain configurations in DNS.
2. Check the Traefik and Docker logs:

```
docker logs <container_id>
```

## Contributing
Feel free to open an issue or pull request for suggestions.

## Follow Me for More Tutorials!

YouTube: [SoftsWeb Channel](https://www.youtube.com/@SoftsWeb)

Website: [SoftsWeb](https://softsweb.com)

## License
This project is open source and available under the MIT License.