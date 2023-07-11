https://itnext.io/kubernetes-storage-part-1-nfs-complete-tutorial-75e6ac2a1f77

# NFS csi driver

Install

curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.4.0/deploy/install-driver.sh | bash -s v4.3.0 --

check pods status:
kubectl -n kube-system get pod -o wide -l app=csi-nfs-controller
kubectl -n kube-system get pod -o wide -l app=csi-nfs-node

Uninstall

curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.4.0/deploy/uninstall-driver.sh | bash -s v4.3.0 --

## Create NFS Server

######################
sudo apt install nfs-common 
sudo mkdir /mnt/nfsshare
sudo mount -t nfs 169.254.96.192:/nfsshare /mnt/nfsshare
######################
# WSL: NFS Server (/nfsshare shared with everyone)
######################
sudo mkdir /nfsshare
sudo chown nobody:nogroup /nfsshare
sudo chmod 777 /nfsshare
sudo sh -c "echo '/nfsshare *(rw,sync,no_subtree_check,insecure)' >> /etc/exports"
sudo service rpcbind start
sudo service nfs-kernel-server start
sudo exportfs -a
######################
# POWERSHELL (as admin): Map ports 443, 2049 to WSL instance on 172.21.29.107 (View your IP with 'ip a | grep eth0')
######################
netsh interface portproxy add v4tov4 listenport=443 listenaddress=0.0.0.0 connectport=443 connectaddress=172.21.29.107
netsh interface portproxy add v4tov4 listenport=2049 listenaddress=0.0.0.0 connectport=2049 connectaddress=172.21.29.107



