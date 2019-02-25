# Kuberpress
Kuberpress is a sample project of deploying a wordpress two tier web application with mysql on Kubernetes with NFS server as persitent volume, Ingress routing and a Python script to store database node ip logs as init container. 

## Steps

### Step 1 - Run NFS server and client
Install nfs-kernel-server on `NFS server` - Ubuntu 18.0.4
```
sudo apt-get update
sudo apt-get install nfs-kernel-server
```
Install nfs-common on `NFS client` - Ubuntu 18.0.4
```
sudo apt-get update
sudo apt-get install nfs-common
```
Create mount directory on `NFS server`.
```
sudo mkdir /var/nfs/general -p
sudo chown nobody:nogroup /var/nfs/general
```
Configure NFS exports on the `NFS server`.
```
sudo nano /etc/exports
```
Assign mount direcoty and client ip address on exports file.
```
/var/nfs/general	172.20.10.5(rw,sync,no_subtree_check,no_root_squash)
```
Then restart `nfs-kernel-server`.
```
sudo systemctl restart nfs-kernel-server
```
Create mount point on `NFS client`
```
sudo mkdir -p /nfs/general
```
Then mount directory on `NFS client`
```
sudo mount 172.20.10.3:/var/nfs/general /nfs/general
```
Now `NFS server` and `NFS client` configured completely.
