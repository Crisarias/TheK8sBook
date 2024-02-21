# Install Fresh Cluster

kind delete cluster --name tkb && kind create cluster --config=kind.yml

# Install Ingress

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

# Install NFS CSI

curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.3.0/deploy/install-driver.sh | bash -s v4.3.0 --

curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.5.0/deploy/install-driver.sh | bash -s v4.5.0 --

apt-get install -y nfs-common
