# Docker Troubleshooting

1. Check Container Status
Use `docker ps -a` to view all containers and their statuses. A container may have exited unexpectedly. 
Look at STATUS and RESTART policies to identify potential issues.

2. Inspect Logs
Run `docker logs <container_name>` to see the container logs. 
This helps troubleshoot crashes, errors, or other issues within the app or service.

3. Debug Interactive Shell
Access a running container’s shell:
docker exec -it <container_name> /bin/bash

This lets you inspect processes and file systems directly.

4. Check Exit Codes
Check the container’s exit code with:

`docker inspect <container_name> --format='{{.State.ExitCode}}'`

Non-zero codes often indicate errors (e.g., code 137 could mean out of memory).

5. Network Troubleshooting
Run docker network ls to list all networks and `docker inspect <container_name>` to see container-specific network settings. 
Use curl or ping inside containers to test network connectivity.

6. Container Restart Policies
Check if the container has been set to restart automatically via --restart. 
The policy can prevent troubleshooting if the container is restarting endlessly:

`docker inspect --format '{{.HostConfig.RestartPolicy.Name}}' <container_name>`

7. File Permissions Issues
Use `docker exec` to check for permission issues inside the container. 
Check logs for errors like "permission denied."

8. Storage & Volume Issues
To check mounted volumes, run:
`docker inspect <container_name> | grep -i volumes`

Ensure the volume is correctly mounted and has appropriate read/write permissions.

9. Rebuild Images
If a container isn’t working as expected, rebuild the image from scratch:
`docker build --no-cache -t <image_name>` .

This clears cached layers and ensures a clean build.

10. Clean Up Dangling Resources
Use docker system prune to remove unused containers, networks, images, and volumes that might clutter your system.

11. Resource Limits
Check CPU and memory limits using `docker inspect <container_name>`. 
Adjust limits via --memory and --cpus flags in the run command.

12. Host System Logs
Look into the host’s logs (e.g., /var/log/syslog or `dmesg`) for Docker daemon errors. 
These can indicate broader system issues affecting containers.

13. DNS Resolution Issues
If containers can’t resolve DNS, use:
`docker run --dns 8.8.8.8`
Or add custom DNS settings in /etc/docker/daemon.json.

14. Port Conflicts
Check if the desired port is already in use:
`sudo lsof -i :<port>`

To resolve conflicts, stop the service using the port or run Docker with different port mappings.

15. Version Compatibility
Ensure Docker and the containerized software versions are compatible. 
Sometimes, upgrading or downgrading Docker versions can resolve bugs.