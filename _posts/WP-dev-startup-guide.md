# WordPress Block Development Startup Guide

A personal checklist for starting a local WordPress block development environment.

---

# Prerequisites

The following software should already be installed.

- Docker Desktop
- Node.js
- npm
- VS Code

---

# Startup Order

Always start the environment in the following order.

```text
1. Docker Desktop
        ↓
2. WordPress (wp-env)
        ↓
3. Webpack Development Server
        ↓
4. Open WordPress in Browser
```

---

# Step 1. Start Docker Desktop

Launch Docker Desktop from macOS.

Wait until Docker reports:

```text
Docker Desktop is running
```

Verify:

```bash
docker ps
```

If Docker is running but WordPress has not started yet, this command may return an empty list.

---

# Step 2. Start WordPress

Move to the project directory.

```bash
cd ~/projects/alfred-affiliate
```

Start the WordPress environment.

```bash
npm run env start
```

This executes:

```text
wp-env start
```

The first startup may take several minutes because Docker images are downloaded.

---

# Step 3. Verify Docker Containers

Check that the containers are running.

```bash
docker ps
```

Expected output:

```text
wordpress
tests-wordpress
mysql
tests-mysql
```

If these containers are running, WordPress is available.

---

# Step 4. Start Webpack

Open another terminal.

Move to the project directory.

```bash
cd ~/projects/alfred-affiliate
```

Start webpack in watch mode.

```bash
npm start
```

Expected output:

```text
webpack compiled successfully
```

Leave this terminal running while developing.

---

# Step 5. Open WordPress

Open the local development site.

```text
http://localhost:8888
```

Open the Block Editor and begin development.

---

# Daily Development Workflow

```text
Start Docker
        ↓
Start wp-env
        ↓
Start webpack
        ↓
Edit code
        ↓
Save
        ↓
Webpack rebuilds automatically
        ↓
Refresh browser
```

---

# Useful Verification Commands

## Current Directory

```bash
pwd
```

---

## List Files

```bash
ls
```

---

## Check package.json

```bash
cat package.json
```

---

## Check Docker Containers

```bash
docker ps
```

---

## Check Running Node Processes

```bash
ps aux | grep node
```

---

## Check Running Docker Containers

```bash
docker container ls
```

---

## Check Docker Images

```bash
docker images
```

---

# Common Problems

## WordPress Does Not Open

Symptoms

- Browser cannot connect
- localhost:8888 is unavailable

Check

```bash
docker ps
```

If no containers are running:

```bash
npm run env start
```

---

## Webpack Is Not Running

Symptoms

- Code changes are not reflected
- No automatic rebuild

Start webpack.

```bash
npm start
```

Expected:

```text
webpack compiled successfully
```

---

## npm start Reports an Error

Verify the current directory.

```bash
pwd
```

Verify that package.json exists.

```bash
ls
```

---

## package.json Is Missing

You are probably in the wrong directory.

Move into the project.

```bash
cd ~/projects/alfred-affiliate
```

---

## Docker Is Not Running

Check.

```bash
docker ps
```

If Docker reports an error or no daemon is available,

Start Docker Desktop first.

---

# Shutdown

Stop webpack

```text
Ctrl + C
```

Stop WordPress

```bash
npm run env stop
```

Or stop everything from Docker Desktop.

---

# Complete Startup Checklist

- Launch Docker Desktop
- `cd ~/projects/alfred-affiliate`
- `npm run env start`
- Verify with `docker ps`
- Open a second terminal
- `cd ~/projects/alfred-affiliate`
- `npm start`
- Wait for `webpack compiled successfully`
- Open `http://localhost:8888`
- Start coding

---

# Frequently Used Commands

```bash
# Move to project
cd ~/projects/alfred-affiliate

# Start WordPress
npm run env start

# Stop WordPress
npm run env stop

# Start webpack
npm start

# Check Docker
docker ps

# Check current directory
pwd

# Check package.json
cat package.json
```

---

# Development Philosophy

Keep the environment simple.

- Docker runs WordPress.
- wp-env manages Docker.
- Webpack builds JavaScript.
- VS Code is the editor.
- The browser is used for testing.

When something does not work, verify each layer one by one instead of guessing.
