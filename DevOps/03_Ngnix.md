# WHAT IS NGINX?
-> It is a lightweight, high-performance web server & reverse proxy server designed to handle high traffic and serve static content efficiently.\
-> NGNIX has grown to include features like Scalability, load balancing, caching, SSL termination, Compression etc.

# WHY NGINX?
Before modern servers:
* Apache used one thread per request
* High memory usage
* Not efficient for large traffic\
NGINX introduced:
* Event-driven architecture
* Asynchronous processing
* Very high performance
* Low memory usage\
That’s why it’s widely used in production.

# WHAT CAN NGINX DO?
-> NGINX can act as:
| Role               | Meaning                     |
| ------------------ | --------------------------- |
| Web Server         | Serve HTML/CSS/JS           |
| Reverse Proxy      | Forward requests to backend |
| Load Balancer      | Distribute traffic          |
| SSL Termination    | Handle HTTPS                |
| API Gateway        | Manage backend APIs         |
| Static File Server | Serve images/files          |
| Caching Server     | Improve performance         |

# PRACTICAL STEPS:
1. Launch your EC2 instance.
2. Install nginx: sudo yum install nginx -y
<img width="930" height="1032" alt="image" src="https://github.com/user-attachments/assets/f32df502-d662-45b1-8b8c-715fcb60867f" />
3. Start your nginx server: sudo systemctl start nginx
<img width="954" height="561" alt="image" src="https://github.com/user-attachments/assets/77f478c3-163a-4330-bd86-05fb92d300b5" />
