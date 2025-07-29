# nginx-docker-proxy-dnsmasq
🧩 Local Reverse Proxy with NGINX + dnsmasq + Docker

This project demonstrates how to create a simple and functional reverse proxy architecture using:

📦 NGINX (as a reverse proxy)

🐳 Docker (for containerized apps)

🌐 dnsmasq (as a local DNS resolver)

It allows you to access applications by clean URLs like http://webapp1.local and http://webapp2.local, without needing to expose ports like :8081 or :8082.

🛠️ What This Setup Includes
A dnsmasq service running on your host to resolve .local domains to your machine's local IP (e.g., 192.168.0.116)

Two NGINX containers as webapps, each serving a simple static HTML page

A main NGINX container configured as a reverse proxy that routes requests based on the domain name

🧪 Example Result
After everything is configured, visiting:

http://webapp1.local will show: WebApp 1 - Proxy Working! 

http://webapp2.local will show: WebApp 2 - Proxy Working!

📁 Project Structure

Docker/
├── nginx-proxy/
│   ├── docker-compose.yml
│   └── nginx.conf
└── webapps/
    ├── docker-compose.yml
    └── webapp1/
    │   └── html/index.html
    └── webapp2/
        └── html/index.html

⚙️ How to Use

1. Install and configure dnsmasq (on your Linux host)

sudo apt install dnsmasq
sudo vim /etc/dnsmasq.d/proxy.conf
add the mappings to your host IP (e.g. 192.168.0.116):
address=/webapp1.local/192.168.0.116
address=/webapp2.local/192.168.0.116
sudo systemctl restart dnsmasq

Test with:
dig webapp1.local @127.0.0.1 +short
You should get back your local IP.

2. Create a shared Docker network

docker network create proxy-net

3. Start the webapps

  cd Docker/webapps
  docker compose up -d

4. Start the NGINX proxy

cd ../nginx-proxy
docker compose up -d

✅ Final Test
Now access:

http://webapp1.local

http://webapp2.local

You should see the expected HTML message from each container, routed through the reverse proxy.

Let me know if you want a version do README em português também, ou um modelo com badges, preview GIF, ou comandos de teardown (docker compose down, etc).
