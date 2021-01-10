Если необходимо изолировать контейнеры в приватную сеть:

```
version: "3"

services:
  server:
    build: server/
    ports:
      - 8081:8081
    networks:
      app_net:
        ipv4_address: 192.168.100.10

  nginx:
    build: nginx/
    ports:
      - 80:80
    networks:
      app_net:
        ipv4_address: 192.168.100.11

    depends_on:
      - server

networks:
  app_net:
    ipam:
      driver: default
      config:
        - subnet: "192.168.100.0/24"
```

Если необходимо привязать в хостовому интерфейсу. 

```
version: "3"

services:
  server:
    build: server/
    network_mode: "host"

  nginx:
    build: nginx/
    depends_on:
      - server
    network_mode: "host"
```
