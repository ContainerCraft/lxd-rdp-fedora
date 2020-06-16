# CloudCTL
Cloud Deployment Administrative Services & Utilities

```
This repo sets up a deployment & administrative actions Kubernetes Pod Yaml defined 
container pod centered around ssh capable ContainerOne with capabilities including
additional container services such as docker registry:2, nginx artifact delivery, etc.
```

# Getting Started
####  1. Install Dependencies
```
On Fedora 32+
  sudo dnf install -y curl ansible python3 python3-pip

On Ubuntu 20.04+
  sudo apt install -y curl ansible python3 python3-pip

On CentOS 8+
  sudo dnf install -y curl python3 python3-pip
  sudo pip3 install --global ansible
```
####  2. Clone Repo
```
git clone https://github.com/containercraft/CloudCTL.git ~/.ccio/Git/cloudctl ; cd ~/.ccio/Git/cloudctl/ansible
```
####  3. Run Ansible
```
./run.yml
```
####  4. Start CloudCtl Pod
```
podman pod create              \
    --name cloudctl            \
    --publish 2022:2022        \
    --pod-id-file ~/.ccio/run/cloudctlPod.id
```
####  4. Start CloudCtl Pod
```
podman run \
    --name one                                                         \
    --userns=keep-id                                                   \
    --detach                                                           \
    --restart always      --pull always                                \
    --volume ${HOME}/.ccio:/root/.ccio:z                               \
    --pod $(cat ~/.ccio/run/cloudctlPod.id)                            \
    --volume ${HOME}/.ssh/authorized_keys:/root/.ssh/authorized_keys:z \
  docker.io/containercraft/one:ccio
```
```
/usr/sbin/sshd -E /dev/stderr -f /etc/ssh/sshd_config -p 2022
```
####  4. Exec into CloudCtl ContainerOne
```
podman pod ps
podman ps -a
```
####  4. Exec into CloudCtl ContainerOne
```
podman exec -it one connect
```
####  5. Disconnect from ContainerOne console
```
quit
```
####  6. Disconnect from ContainerOne console
```
podman pod rm --force cloudctl
```
