## Installing Docker

To install Docker CE on Raspbian Jessie/Stretch:

```bash
# Install some required packages first
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install -y \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common

# Get the Docker signing key for packages
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -

# Add the Docker official repos
echo "deb [arch=armhf] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list

# Install Docker
sudo apt-get update
sudo apt-get install -y docker-ce

# Start docker service
sudo systemctl enable docker
sudo systemctl start docker

# optional: run a test image
sudo docker run --rm arm32v7/hello-world
```

[link to Original Instructions](https://withblue.ink/2017/12/31/yes-you-can-run-docker-on-raspbian.html), thanks to _Alessandro Segala_.
