# Reverse Proxy

## What is a reverse proxy?
A reverse proxy intercepts requests from clients and forwards them to backend servers. It acts as an intermediary for resources provided by a server, making it appear as though clients are directly interacting with the proxy.

## Why implement one?
Reverse proxies offer several benefits:
- **Load Balancing**: Distributes incoming traffic across multiple servers to optimize performance.
- **Security**: Protects backend servers by masking their identity and shielding them from direct exposure.
- **Caching**: Speeds up response times for clients by storing frequently accessed data.
- **Compression**: Compresses data before sending it to clients for better network efficiency.

## How are they different from forward proxies?
- **Forward Proxy**: Acts on behalf of clients, intercepting client requests and forwarding them to servers. It hides the identity of clients from servers.
- **Reverse Proxy**: Acts on behalf of servers, intercepting client requests and forwarding them to backend servers. It focuses on protecting and enhancing server functionality.

## How do reverse proxies work?
1. A client sends a request to the reverse proxy.
2. The reverse proxy examines the request and determines which backend server to forward it to.
3. The backend server processes the request and sends a response back to the reverse proxy.
4. The reverse proxy forwards the response to the client.

![reverse proxy](image.png)


# Implementation

## Assumptions
- nginx is running with default config
- the backend app is running 

## 1. Edit ```default``` (config file)
```sudo sed -i "51c\proxy_pass http://0.0.0.0:3000;" /etc/nginx/sites-available/default```

> `sed` = "Stream Editor" used to edit the text
> 
> `-i` = Edit the file in-place
> 
> `51c\` = Change line 51
> 
> `proxy_pass http://0.0.0.0:3000;` = The line to add
> 
> > Use 0.0.0.0 to accept all incoming connections associated with the host e.g. its public IP
> 
> `/etc/nginx/sites-available/default` = The path to the config file

## 2. Restart nginx 
```sudo systemctl restart nginx```