# Restore database

```
docker-compose stop neo4j
```

Restore old database
```
mkdir -p $HOME/neo4j/dumps

docker run --interactive --tty --rm \
  --volume /$HOME/neo4j/data:/data \
  --volume $HOME/neo4j/dumps/2025.12.28-PTLinks-neo4j.dump:/dumps/neo4j.dump \
  neo4j:latest \
  neo4j-admin database load neo4j --from-path=/dumps --overwrite-destination=true --verbose

# Migrate database (if restoring from Neo4j 4.x to Neo4j 5.x)
docker run --interactive --tty --rm \
  --volume /$HOME/neo4j/data:/data \
  neo4j:latest \
  neo4j-admin database migrate neo4j --force-btree-indexes-to-range
```