# Networking for DevOps and Docker

Networking is one of the most critical DevOps foundations. Most production outages are caused not by code, but by networking misconfigurations involving ports, DNS, firewalls, routing, or container networking.

---

## 1. Core Networking Concepts for DevOps

Every DevOps engineer must clearly understand:

- IP Address – identifies a machine or container
- Port – entry point for a service
- Protocol – TCP, UDP, HTTP, HTTPS
- DNS – resolves names to IPs
- Firewall – controls allowed traffic

These concepts apply equally to Linux servers, containers, and cloud platforms.

---

## 2. Linux Networking Essentials

Check network interfaces and IPs:

```bash
ip addr
````

Check routing table:

```bash
ip route
```

Check listening ports and active connections:

```bash
ss -tuln
```

Test basic connectivity:

```bash
ping google.com
```

Verify DNS resolution:

```bash
nslookup google.com
```

These commands are used during almost every incident investigation.

---

## 3. Common Networking Troubleshooting Flow

When an application is unreachable:

1. Check if the service is running
2. Verify the correct port is listening
3. Test connectivity from the host
4. Check firewall rules
5. Verify DNS resolution
6. Inspect routing and network policies

Skipping steps leads to misdiagnosis.

---

## 4. Docker Networking Overview

Docker uses virtual networks to allow container communication.

Default Docker network types:

* bridge – default isolated network
* host – container shares host networking
* none – no networking

List Docker networks:

```bash
docker network ls
```

Inspect a network:

```bash
docker network inspect bridge
```

Understanding Docker networking prevents service-to-service failures.

---

## 5. Container-to-Container Communication

Containers on the same Docker network communicate using container names.

Example:

```bash
docker network create app-net
docker run -d --name backend --network app-net backend-image
docker run -d --name frontend --network app-net frontend-image
```

`frontend` can reach `backend` using DNS name `backend`.

This is the foundation of microservices communication.

---

## 6. Port Mapping and Exposure

Expose container ports to the host:

```bash
docker run -p 8080:80 nginx
```

* Host port: 8080
* Container port: 80

Incorrect port mapping is one of the most common Docker issues.

---

## 7. Debugging Networking Inside Containers

Access a running container:

```bash
docker exec -it container_name sh
```

Test connectivity from inside:

```bash
ping backend
curl http://backend:8080
```

Always debug from inside the container, not just the host.

---

## 8. DNS Behavior in Docker

Docker provides an internal DNS server for containers on the same network.

Check DNS configuration:

```bash
cat /etc/resolv.conf
```

DNS issues often appear as application failures rather than network errors.

---

## 9. Firewalls and Network Security Basics

Common firewall tools:

* iptables
* firewalld
* cloud security groups

Check firewall status:

```bash
sudo iptables -L
```

Blocked ports frequently cause production outages.

---

## 10. Real-World DevOps Networking Issues

Common failures include:

* Service running but port not exposed
* DNS misconfiguration between containers
* Firewall blocking internal traffic
* Wrong network attached to container
* Incorrect load balancer target port

Most “application down” issues are networking-related.

---

## 11. DevOps Networking Best Practices

* Never hardcode IP addresses
* Use DNS-based service discovery
* Limit exposed ports
* Monitor network latency and errors
* Always test connectivity end-to-end

Strong networking fundamentals prevent silent production failures.
