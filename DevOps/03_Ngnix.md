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
4. Copy the public ip of your VM and runin browser, it will show:
<img width="310" height="139" alt="image" src="https://github.com/user-attachments/assets/afb5d336-fce5-4314-92f0-6e0a380ce487" />

# NGINX CONFIGS:
-> Main config file: /etc/nginx/nginx.conf
<img width="895" height="855" alt="image" src="https://github.com/user-attachments/assets/636e427f-1982-4ab4-848b-87dd1c91820f" />
<img width="305" height="414" alt="image" src="https://github.com/user-attachments/assets/3038ab95-63ad-4890-b2dd-b96994c024ee" />\
-> When you ran: ls\
You saw important files:\
nginx.conf - Main Nginx configuration file\
conf.d/ -	Directory for additional server block configs\
default.d/ -	Default config snippets\
mime.types -	Maps file extensions to content types\
fastcgi_params -	Used for PHP/FastCGI configuration\
uwsgi_params -	Used for Python uWSGI apps\
scgi_params -	Used for SCGI apps\
 * Understanding nginx.conf Structure:

You displayed:

cat nginx.conf

Let’s break it down clearly.

🔹 Global Settings
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;
Meaning:

user nginx; → Nginx worker processes run as nginx user

worker_processes auto; → Uses CPU cores automatically

error_log → Location of error logs

pid → Process ID file location

🔹 Load Dynamic Modules
include /usr/share/nginx/modules/*.conf;

Loads additional modules dynamically.

🔹 Events Block
events {
    worker_connections 1024;
}

Controls connection handling

1024 = max simultaneous connections per worker

🔹 HTTP Block (Most Important Section)

Everything related to web traffic is inside:

http { }
Includes:
📌 Log Format
log_format main ...
access_log /var/log/nginx/access.log main;

Defines how logs are stored

Access logs saved in /var/log/nginx/access.log

📌 Performance Settings
sendfile on;
tcp_nopush on;
tcp_nodelay on;
keepalive_timeout 65;

These improve performance and TCP efficiency.

📌 MIME Types
include /etc/nginx/mime.types;
default_type application/octet-stream;

Defines content types like:

.html → text/html

.css → text/css

.js → application/javascript

📌 Load Virtual Hosts
include /etc/nginx/conf.d/*.conf;

This means:

👉 Any .conf file inside conf.d/ becomes a server block.

Professional practice:
Never modify main nginx.conf.
Create new configs inside conf.d/.

4️⃣ Default Server Block

Inside nginx.conf, you saw:

server {
    listen 80;
    server_name _;
    root /usr/share/nginx/html;
}
Meaning:

listen 80; → Listens on HTTP port

server_name _; → Default server (catch-all)

root /usr/share/nginx/html; → Website files location

5️⃣ Default Website Directory

You tried:

cd /usr/share/nginx.html

❌ Wrong path

Correct path:

/usr/share/nginx/html

This is defined in:

root /usr/share/nginx/html;

When you listed files:

404.html
50x.html
index.html

This index.html is what your browser is showing.

6️⃣ Viewing Website Content

You ran:

less index.html

That shows the HTML source of the default Nginx page.

7️⃣ Important Nginx File Locations Summary
Purpose	Path
Main config	/etc/nginx/nginx.conf
Virtual hosts	/etc/nginx/conf.d/
Default web root	/usr/share/nginx/html/
Access logs	/var/log/nginx/access.log
Error logs	/var/log/nginx/error.log
8️⃣ Correct Way to Edit Config

Always:

sudo nano /etc/nginx/conf.d/myapp.conf

Then test before reload:

sudo nginx -t

If OK:

sudo systemctl reload nginx
9️⃣ Important DevOps Concepts You Practiced

✔ Linux file permissions
✔ Root vs normal user
✔ Nginx configuration structure
✔ Server blocks
✔ Default document root
✔ Log management
✔ Modular config system

🔥 Interview-Level Summary

Nginx configuration is divided into:

Global configuration

Events block

HTTP block

Server blocks

Location blocks

It follows a hierarchical configuration model.
