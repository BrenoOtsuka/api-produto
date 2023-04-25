### Executar com Docker Compose

```
 docker compose --env-file ./.env up -d --build
```

### Executar sem Docker Compose

Docker Network

```
docker network create produto_net
```

MongoDB Container

```
docker container run -d -p 27017:27017      \
    -e MONGO_INITDB_ROOT_USERNAME=mongouser \
    -e MONGO_INITDB_ROOT_PASSWORD=mongopwd  \
    -v mongo_vol:/data/db                   \
    --network produto_net                   \
    --name mongodb                          \
    mongo:4.4.3
```

App Container

```
docker container run -d -p 8080:8080                                \
    --network produto_net                                           \
    -e MONGODB_URI=mongodb://mongouser:mongopwd@mongodb:27017/admin \
    brenootsuka/api-produto:v1
```

App URL

http://localhost:8080/api-docs
