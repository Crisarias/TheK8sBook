https://mohitgoyal.co/2021/03/19/setup-local-kubernetes-cluster-with-docker-wsl2-and-kind-part-2/

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-rc6/aio/deploy/recommended.yaml

kubectl create -f dashboard.admin-user.yml -f dashboard.admin-user-role.yml

kubectl -n kubernetes-dashboard create token admin-user

kubectl -n kubernetes-dashboard describe secret admin-user-token | grep ^token

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
