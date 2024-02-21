# WEBDAV: Mounting with rclone

## Setup rclone

Download the `rclone` binary with your package manager.

Create a directory to mount to:

```bash
mkdir ~/mounts/[NAME]
```

Create a `rclone` config by typing:

```bash
rclone config
```

Answer the questions in the prompts:

```
No remotes found, make a new one?
> n

Enter name for new remote.
> [NAME]

Type of storage to configure.
> 52 (whichever is WebDAV)

URL
> [WEBDAV URL]

Name of the WebDAV site/service/software you are using.
> 6 (whichever is rclone)

User name.
> [USERNAME/EMAIL]

Password.
> y

Enter the password:
> [TOKEN]

Confirm the password:
> [TOKEN]

Option bearer_token.
> (nothing, press enter)

Edit advanced config?
→ n

Keep this "[NAME]" remote?
→ y

Current remotes
→ q
```
To mount the drive:
```bash
rclone mount [NAME]:/ /your/mount/point --vfs-cache-mode full --daemon
```
## Setup Automatic Mounting

1. Create a systemd service file:

```bash
sudo vi /etc/systemd/system/rclone-name.service
```

2. Add the following content to the file:

```ini
[Unit]
Description=RClone NAME Mount

[Service]
Type=simple
ExecStart=/path/to/rclone mount NAME:/ /home/yourusername/your/mount/point --vfs-cache-mode full
ExecStop=/bin/fusermount -uz /home/yourusername/path/to/mountpoint
Restart=on-abort
User=yourusername
Group=yourusername

[Install]
WantedBy=default.target
```

Replace `/path/to/rclone` with the actual path to your `rclone` binary, and `yourusername` with your actual username.

3. Save the file and exit the text editor.

4. Reload systemd:

```bash
sudo systemctl daemon-reload
```

5. Enable the service to run at startup:

```bash
sudo systemctl enable rclone-name.service
```

6. Start the service:

```bash
sudo systemctl start rclone-name.service
```

Now, your rclone mount command should run automatically on login. You can also manually start, stop, or restart the service using the `systemctl` command:

- Start the service: `sudo systemctl start rclone-name.service`
- Stop the service: `sudo systemctl stop rclone-name.service`
- Restart the service: `sudo systemctl restart rclone-name.service`

Make sure to adapt the paths and usernames in the service file to match your system configuration.
