# DISTROBOX: Guide

## Resources

- [Learn Linux TV: Distrobox Tutorial](https://www.youtube.com/watch?v=eiDt4O6UPRw)

## Installation (Debian Systems)

1. Add the [Distrobox PPA Repository](https://launchpad.net/~michel-slm/+archive/ubuntu/distrobox)
2. Install podman: `sudo apt install podman`
3. Install distrobox: `sudo apt install distrobox`

## Creating and Managing Containers

- Create a new container:

  ```bash
  distrobox create --name <container_name> --image <image_name>
  ```

- Enter a container:

  ```bash
  distrobox enter <container_name>
  ```

- List all containers:

  ```bash
  distrobox list
  ```

- Remove a container:

  ```bash
  distrobox rm <container_name>
  ```

- Stop a running container:

  ```bash
  distrobox stop <container_name>
  ```

## Exporting Applications

- Export an application from container to host:

  ```bash
  distrobox-export --app <application_name>
  ```

- Export a binary from container to host:

  ```bash
  distrobox-export --bin <binary_path>
  ```

## Container Management

- Upgrade all containers:

  ```bash
  distrobox upgrade --all
  ```

- Upgrade a specific container:

  ```bash
  distrobox upgrade <container_name>
  ```

## Additional Features

- Execute a command in a container:

  ```bash
  distrobox-enter <container_name> -- <command>
  ```

- Generate a desktop entry for an application:

  ```bash
  distrobox-export --app <application_name> --extra-flags "--generate-desktop-entry"
  ```

- List exported applications:

  ```bash
  distrobox-export --list
  ```

- Remove an exported application:

  ```bash
  distrobox-export --app <application_name> --delete
  ```

## Example: Debian Dev Container

### Step 1: Install Distrobox

Installation instructions on the [Distrobox GitHub page](https://github.com/89luca89/distrobox).

### Step 2: Create the Container

1. **Create the Container with a Separate Home Directory**

   Run the following command to create a container named `devcontainer` using the latest stable version of Debian and a separate home directory:

   ```bash
   distrobox create --name devcontainer --image debian:stable --home ~/distrobox/devcontainer_home
   ```

2. **Enter the Container**

   Enter the container you just created:

   ```bash
   distrobox enter devcontainer
   ```

### Step 3: Install Components

 Inside the devcontainer, install `gcc` and `git`:

 ```bash
 sudo apt install gcc git
 ```

