Is an open source (BSD licensed), in-memory **data structure store** used as a [[database]], [[cache]], message broker, and streaming engine.
## Docker setup
```yml
services:
	redis-stack:
		image: redis/redis-stack:7.2.0-v2
		container_name: redis
		ports:
			- '6379:6379'
			- '8001:8001'
```

To start a communication with it:
```zsh
docker exec -it redis redis-cli

127.0.0.1:6379> ping
PONG
127.0.0.1:6379> 
```
