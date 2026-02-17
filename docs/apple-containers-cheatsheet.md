# Apple: Container CLI Cheatsheet

## ⚙️ System Setup

**Start Service (Required):**

```bash
% container system start 
```

**Stop Service (Recommended):** 

```bash
% container system stop 
```

**Verify Installation:**

```bash
% container --version 
```

## 🖼️ Image Management

**Pull Image:** 

```bash
% container image pull debian:latest 

```

**List Images:** 

```bash
% container images 
```

**Build Images:** 

```bash
% container image build -t myapp . 
```

**Delete Images:** 

```bash
% container image delete <image-name> 
```

## ▶️ Container Operations

**Run Interactive Shell:** 

```bash
% container run -it debian:latest /bin/bash 
```

**Run & Name:** 

```bash
% container run -it --name my-server ubuntu:latest 
```

**Run & Clean Up** (Removes container upon exit)**:** 

```bash
% container run --rm alpine:latest echo "done" 
```

**Port Forwarding** (Maps host 8080 to container 80)**:** 

```bash
% container run -d -p 8080:80 nginx:latest 
```

## 🛑 Container Control & Cleanup

**List Running Containers:** 

```bash
% container list 
```

**List All Containers (Running & Stopped):** 

```bash
% container list -a 
```

**Stop Container:** 

```bash
% container stop <name-or-id> 
```

**Start Container:** 

```bash
% container start <name-or-id> 
```

**Attach to Running Shell:** 

```bash
% container attach <name-or-id> 
```

**Delete Container:** 

```bash
% container delete <name-or-id> 
```

**Clean Up All Stopped Containers** (Use with caution)**:** 

```bash
% container delete $(container list -a -q)
```
