## MonAst with PJSIP in Docker  
MonAst with patch for PJSIP support.  
Original MonAst: [Repository](https://github.com/dagmoller/monast)
### Install  
Create `.env` file:  
```
VOIP_IP="" # VOIP Instance IP
VOIP_USER="" # AMI User
VOIP_PASS="" # AMI Password
MONAST_PASS="" # MonAst admin password
```
Get `docker-compose.yml` file:  
```
services:
 monast-pymon0:
  build:
    context: ./pymon
    dockerfile: Dockerfile
  image: ghcr.io/scorpionukr/monast-pymon:latest
  container_name: monast-pymon0
  environment:
    - ASTERISK_HOST=${VOIP_IP}
    - ASTERISK_PORT=5038
    - AMI_USERNAME=${VOIP_USER}
    - AMI_PASSWORD=${VOIP_PASS}
    - USER_ADMIN_SECRET=${MONAST_PASS}
  networks:
    - monast-net

 monast-php:
  build:
    context: ./php
    dockerfile: Dockerfile
  image: ghcr.io/scorpionukr/monast-php:latest
  container_name: monast-php0
  depends_on:
    - monast-pymon0
  ports:
    - "8080:80"
  environment:
    - PYMON_HOST=monast-pymon0
  networks:
    - monast-net

networks:
  monast-net:
    driver: bridge
    driver_opts:
      com.docker.network.enable_ipv6: "false"
    ipam:
      driver: default
      config:
      - subnet: 192.168.201.0/24
        gateway: 192.168.201.1
```
Build image:  
```
docker compose build --no-cache
```
Start the Service:  
```
docker compose up -d
```

**If you find this project useful or inspiring, please support it with a donation.**  
[<img src="https://felen.io/static/img/felen_whole_logo.png" width="20%" />](https://felen.io/fraglist/pay/)