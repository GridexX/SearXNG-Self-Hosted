<div align="center">

  <img src="assets/logo.png" alt="logo" width="200" height="auto" />
  <h1>SearXNG SelfHosted</h1>
  
  <p>
    Deploy easily your SearXNG instance!
  </p>

  
  
<!-- Badges -->
<p>
  <a href="https://github.com/GridexX/SearXNG-Self-Hosted/graphs/contributors">
    <img src="https://img.shields.io/github/contributors/GridexX/SearXNG-Self-Hosted" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/GridexX/SearXNG-Self-Hosted" alt="last update" />
  </a>
  <a href="https://github.com/GridexX/SearXNG-Self-Hosted/network/members">
    <img src="https://img.shields.io/github/forks/GridexX/SearXNG-Self-Hosted" alt="forks" />
  </a>
  <a href="https://github.com/GridexX/SearXNG-Self-Hosted/stargazers">
    <img src="https://img.shields.io/github/stars/GridexX/SearXNG-Self-Hosted" alt="stars" />
  </a>
  <a href="https://github.com/GridexX/SearXNG-Self-Hosted/issues/">
    <img src="https://img.shields.io/github/issues/GridexX/SearXNG-Self-Hosted" alt="open issues" />
  </a>
  <a href="https://github.com/GridexX/SearXNG-Self-Hosted/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/GridexX/SearXNG-Self-Hosted.svg" alt="license" />
  </a>
</p>
   
</div>

<br />


## Description

SearXNG

This repository aims to create a new SearXNG instance in five minutes using Docker containers.
It provides a combination with Nginx Proxy Manager to creates a SSL endpoint to your instance.

## How to Deploy this repo ?

### Prerequisites

- `Docker` ~ 20
- `Git`

### Commands

```bash
  # Clone the repo
  git clone git@github.com:GridexX/SearXNG-Self-Hosted.git

  # Move in the main directory
  cd SearXNG-Self-Hosted

  # Replace the Secret Key used by SearchXNG
  sed -i "s|ultrasecretkey|$(openssl rand -hex 32)|g" searxng/settings.yml

  # Start the containers
  docker compose up -d
```

## Reverse Proxy with Nginx Proxy Manager

To add a custom Domain Name with a SSL endpoint, a docker compose file is provided in this repository.
Here are the steps to reproduce:

1. Uncomment the line in the network file in the `docker-compose.yml` file:

    ```docker
    networks:
      searxng:
        ipam:
          driver: default
      nginx-proxy-manager_web-proxy: # If you want to use Nginx Proxy Manager network
        external: true
    ```

2. Start the NPM instance:

    ```bash
    docker compose up -f docker-compose-npm.yml up -d 
    ```

3. Start the SearXNG stack:

    ```bash
    docker compose up -d
    ```

4. Creates the DNS record from your DNS manager with your `DOMAIN`
5. Add the Proxy Host on NPM
  Use the following settings:
     - **Scheme**: `http`
     - **Forward Hostname / IP**: `searxng.dockerlocal`
     - **Port**: `8080`

    Create a new SSL certificates and check:

    - **Force SSL**
    - **HTTP/2 Support**
    - **HSTS enabled**

  Well done you finished the configuration 🥳  
  Now go on your `DOMAIN` url, you should see the HomePage !

## Reference

This repository is heavily inspired by the [searxng-docker](https://github.com/searxng/searxng-docker) repository.

For more information about how to configure proxy hosts, refers to the [NPM documentation](https://nginxproxymanager.com/)

## Author

Redacted by [@GridexX](https://github.com/gridexx) during a scorching day in Iasi 🥵🇷🇴
