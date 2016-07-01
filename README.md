Please follow below guide, then start private Docker registry by **docker-compose**!

## Environment
CentOS 7.2, Docker version 1.11.2, Docker compose 1.7.1 & registry:v2 image

## Private Docker registry solutions
1. Proxy with HTTP
2. Non-Proxy registry with HTTP
3. Proxy with HTTPS
4. Non-Proxy with HTTPS

## HTTPS Pre-conditions
1. Add a domain name for the registry, ex: docker-proxy
2. Generate a cert for the domain (Common Name/CN)

  ```
  openssl req -newkey rsa:4096 -nodes -sha256 -keyout docker-proxy.key -x509 -days 1000 -out docker-proxy.crt
  ```

3. Update the cert for curl HTTPS operation

  ```
  update-ca-trust force-enable
  cp docker-proxy.crt /etc/pki/ca-trust/source/anchors/
  update-ca-trust extract
  ```

## Operations
1. Check images in registry

  ```
  curl http://<domain-name>:<port>/v2/_catalog
  curl https://<domain-name>:<port>/v2/_catalog
  ```

2. Push image to regsitry

  ```
  docker login <domain-name>:<port>
  docker push <domain-name>:<port>/<image-name>[:<optinal tag>]
  ```

3. Pull image from registry

  ```
  docker pull <domain-name>:<port>/<image-name>[:<optinal tag>]
  ```
