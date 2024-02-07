Nginx is a [[Web]] server software that helps manage and deliver web content. Think of it like a traffic cop for the internet – it receives requests from users' web browsers and directs them to the appropriate website or web application. Nginx is known for its speed and efficiency, making websites load quickly and handle a large number of users at the same time. It can also perform other tasks, like load balancing to distribute incoming traffic across multiple servers, and act as a reverse proxy to enhance security. In simple terms, Nginx is a key player in making the internet work smoothly and efficiently.

Nginx operates on a master-worker architecture. Here's a brief explanation:

1. **Master Process:**
    - The master process is the main control process that manages the overall operation of Nginx.
    - It reads and evaluates configuration files, and it's responsible for starting, reloading, and stopping the worker processes.
    - The master process doesn't handle the actual handling of client requests or serving content; it delegates these tasks to the worker processes.
    
2. **Worker Processes:**
    - Worker processes are responsible for handling client requests and serving content.
    - Multiple worker processes can run simultaneously to take advantage of multi-core systems, improving performance and concurrency.
    - Each worker process operates independently, and they share the load of processing incoming requests.
    - If one worker becomes unresponsive or encounters an issue, it doesn't affect the entire server since the other workers continue to function.

The master-worker architecture of Nginx allows it to efficiently handle a large number of simultaneous connections and distribute the workload across multiple processes. This design enhances performance, scalability, and reliability by isolating tasks and providing a way to balance the processing load.

Configuration example:
```nginx
worker_processes auto;

events {
	worker_connections 4096;
}

http {
	access_log off;
	error_log /dev/null emerg;
	
	upstream api {
		server localhost:9501;
		server localhost:9502;
		keepalive 400;
	}
}
```

- `worker_processes auto;` evaluates how many CPUs the machine has and starts worker instances 1.5 times.
- `worker_connections 4096;` Sets the number of connections per worker. Nginx organizes the responses from each connection into a queue so that all connections are served. You can set an timeout for each request in this queue.
- Nginx only receives requests, processing and responding is the responsibility of servers registered in `upstream api`.