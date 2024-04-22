# Comment utiliser docker-compose

```bash
touch docker-compose.yml
echo '''version: '3.9'
services:
  back:
    ...''' > docker-compose.yml
docker-compose up # Pour lancer docker-compose
```

Voici des exemple de docker-compose file:

```
https://docs.docker.com/compose/
https://docs.docker.com/compose/compose-application-model/
```

# Télécharger une image Docker pour votre base de données

Pour utiliser une base de données dans un environnement Docker, vous pouvez télécharger des images Docker préconfigurées depuis Docker Hub. Voici quelques exemples pour différentes bases de données :

```yaml
redis: https://hub.docker.com/_/redis
mongo: 
  - mongo: https://hub.docker.com/_/mongo
  - mongo-express: https://hub.docker.com/_/mongo-express
mysql: https://hub.docker.com/_/mysql
mariadb: https://hub.docker.com/_/mariadb
```

# Lier votre base de données et votre serveur web sur le réseau Docker

Vous devrez utilisé les intefaces réseaux docker afin de permettre la communication 
de manière privé entre vos conteneur

```yaml
version: '3.9'
services:
  back:
    ...
    networks:
      private_net:
        ipv4_address: 172.100.30.2

  db:
    ...
    networks:
      private_net:
        ipv4_address: 172.100.30.3

networks:
  private_net:
    driver: bridge
    ipam:
      config:
        - subnet: 172.100.30.0/24
          gateway: 172.100.30.1
```