# ksgpu


## Prerequisite

### 1. Install `ansible`


### 2. Install `cfssl` on local machine

* Linux: 

```bash
wget -q --show-progress --https-only --timestamping  https://pkg.cfssl.org/R1.2/cfssl_linux-amd64 \
      https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64
  chmod +x cfssl_linux-amd64 cfssljson_linux-amd64
  sudo mv cfssl_linux-amd64 /usr/local/bin/cfssl
  sudo mv cfssljson_linux-amd64 /usr/local/bin/cfssljson
```

### 3. Setup passwordless login from client to all hosts

```bash
ssh-keygen 
# three Enters

# copy the key to each host:
ssh-copy-id -i ~/.ssh/id_rsa host1
ssh-copy-id -i ~/.ssh/id_rsa host2
...
```

### 4. Make user a sudoer without password

On each hosts:

```
sudo visudo
# Insert the line
username ALL=(ALL) NOPASSWD:ALL
```



## Run

```bash
ansible-playbook -i hosts site.yaml
```