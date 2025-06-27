# Distributed-edge-mini-cloud-Docker

A single, multi-arch Docker image that bundles and orchestrates:

- **Nextcloud** (self-hosted file sync & share)  
- **Grafana** (metrics dashboards)  
- **Prometheus** (metrics collection)  
- **Jupyter Notebook** (interactive Python notebooks)  
- **Samba** (SMB file shares)  
- **Custom LLM UI** (your chat interface)  
- **Static websites** (your `website/` and `chat-ui/` folders)

Built for both **linux/amd64** and **linux/arm64**.

---

## Links

Github link for all files inside:
[Image files](https://github.com/IrfanUruchi/Edge-Distributed-Mini-Cloud-System)

Docker Hub [Main node Docker Image](https://hub.docker.com/r/irfanuruchi/distributed-edge-mini-cloud)

Docker Hub 2: [Link for Node 2](https://hub.docker.com/r/irfanuruchi/llm-proxy)


If any issue arrises or you want to contribute feel free to use this GitHub Repo to report bugs or suggest improvements.

---
## Quick start

**Pull:**

```bash
docker pull irfanuruchi/distributed-edge-mini-cloud:0.1.1
```

**Run:**

```bash

docker run -d --name mini-cloud \
  -p 80:8080    \  # Nextcloud (Apache)  
  -p 3000:3000  \  # Static chat-ui  
  -p 3001:3001  \  # LLM UI 
  -p 8086:8086  \  # Prometheus  
  -p 8888:8888  \  # Jupyter  
  -p 139:139    \  # Samba (SMB port 1)  
  -p 445:445    \  # Samba (SMB port 2)  
  -v mini-cloud-data:/data \
  irfanuruchi/distributed-edge-mini-cloud:0.1.1
```

Once started, your services are available (assuming you used the Run code provided):

- Nextcloud in port 8080 using http://<host>:8080 to access it
- Static Chat-UI in port 3000 using http://<host>:3000 to access it
- LLM UI in port 3001(assuming you are using the other docker image for making the system distributed) using http://<host>:3001
- Prometheus in port 8086 using http://<host>:8086 to access it
- Jupyter Notebook in port 8888 using using http://<host>:8888 for accessing the python code ui
- Samba SMB share from either SMB port 1 or 2 using the SMB and not the http protocol.

---

## Features & Persistence

- All-in-one container
- Persistent data
- Multi-arch support
- Private LLMs and data sharing feature

## Configuration

You can override defaults via environment variables:

- NC_ADMIN / NC_PASS – Nextcloud admin username & password

- TZ – Container timezone (default: Europe/Skopje)

**Example:**

Use this if you are in a different time zone and want different username/password (dont forget to change NC_ADMIN and NC_PASS to your prefered and also the timezone TZ to where you are)

```bash
docker run -d --name mini-cloud \
  -e NC_ADMIN=admin -e NC_PASS=secret \
  -e TZ=America/New_York \
  -p 80:8080 -p 3000:3000 -p 3001:3001 \
  -p 8086:8086 -p 8888:8888 -p 139:139 -p 445:445 \
  -v mini-cloud-data:/data \
  irfanuruchi/distributed-edge-mini-cloud:latest
```
---

## Licence

This repo (and the other one) are MIT-Licensed.

