# Deploy sql database with docker

## For deploy the database image :

```
docker run --name fleet_database -v "$PWD/db_fleet_data":/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -e MYSQL_DATABASE=fleet -dp 3306:3306 mysql:latest
```

## To enter in bash of docker :

```
docker exec -it fleet_database bash
```

## Creating database tables :

```
docker exec -i fleet_database sh -c 'exec mysql -u root -p"$MYSQL_ROOT_PASSWORD" fleet' < ./create-table-template.sql
```

## Creating database dumps :

```
docker exec fleet_database sh -c 'exec mysqldump -u root -p"$MYSQL_ROOT_PASSWORD" fleet' > ./fleet_databases.sql
```

## Restoring data from dump files :

```
docker exec -i fleet_database sh -c 'exec mysql -u root -p"$MYSQL_ROOT_PASSWORD" fleet' < ./fleet_databases.sql

```
