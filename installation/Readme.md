# Install Fresh Cluster

kind delete cluster --name tkb && kind create cluster --config=kind.yml

# Install Ingress

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
