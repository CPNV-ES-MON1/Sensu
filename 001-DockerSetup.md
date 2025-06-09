# 001-DockerSetup

* [Debian Official Documentation](https://docs.docker.com/engine/install/debian/)

* Uninstall old Docker version and librairies

```
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

* Get archives

Note : using the standard apt install was not possible due to missing public key

```
wget https://download.docker.com/linux/debian/dists/bookworm/pool/stable/amd64/containerd.io_1.7.27-1_amd64.deb
wget https://download.docker.com/linux/debian/dists/bookworm/pool/stable/amd64/docker-buildx-plugin_0.24.0-1~debian.12~bookworm_amd64.deb
wget https://download.docker.com/linux/debian/dists/bookworm/pool/stable/amd64/docker-ce-cli_28.2.2-1~debian.12~bookworm_amd64.deb
wget https://download.docker.com/linux/debian/dists/bookworm/pool/stable/amd64/docker-ce_28.2.2-1~debian.12~bookworm_amd64.deb
wget https://download.docker.com/linux/debian/dists/bookworm/pool/stable/amd64/docker-compose-plugin_2.36.2-1~debian.12~bookworm_amd64.deb
wget https://download.docker.com/linux/debian/dists/bookworm/pool/stable/amd64/docker-model-plugin_0.1.24-1~debian.12~bookworm_amd64.deb
wget https://download.docker.com/linux/debian/dists/bookworm/pool/stable/amd64/docker-scan-plugin_0.23.0~debian-bookworm_amd64.deb
```

* Uncompress archives

```
sudo dpkg -i ./containerd.io_1.7.27-1_amd64.deb \
  ./docker-ce_28.2.2-1~debian.12~bookworm_amd64.deb \
  ./docker-ce-cli_28.2.2-1~debian.12~bookworm_amd64.deb \
  ./docker-buildx-plugin_0.24.0-1~debian.12~bookworm_amd64.deb \
  ./docker-compose-plugin_2.36.2-1~debian.12~bookworm_amd64.deb
```

* Start and test Docker

```
sudo service docker start
sudo docker run hello-world
```

