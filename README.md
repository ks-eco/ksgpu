# ksgpu

Deploy a (GPU-enabled) production-ready kubernetes cluster.

## Prerequisite

### 1. Install `ansible` on local deploy machine

```bash
(sudo) pip3 install ansible
```

### 2. Install `cfssl` on local deploy machine

* Linux:

```bash
wget -q --show-progress --https-only --timestamping https://pkg.cfssl.org/R1.2/cfssl_linux-amd64 \
      https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64
  chmod +x cfssl_linux-amd64 cfssljson_linux-amd64
  sudo mv cfssl_linux-amd64 /usr/local/bin/cfssl
  sudo mv cfssljson_linux-amd64 /usr/local/bin/cfssljson
```

### 3. Setup passwordless login from client to all hosts

```bash
ssh-keygen
# three Enters

# copy the key to each host (replace host* with real hostnames)
ssh-copy-id -i ~/.ssh/id_rsa host1
ssh-copy-id -i ~/.ssh/id_rsa host2
...
```

### 4. Make user a sudoer without password

On each hosts:

```
sudo visudo
# Insert the line (replace username with real username)
username ALL=(ALL) NOPASSWD:ALL
```

## Run

```bash
# Just check syntax:
ansible-playbook site.yaml --syntax-check -i hosts
# list hosts
ansible-playbook site.yaml --list-hosts -i hosts
```

```bash
ansible-playbook --ask-become-pass -i hosts site.yaml
```
