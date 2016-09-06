

git clone https://github.com/kubernetes/kubernetes.git

kubectl create -f examples/guestbook/redis-master-deployment.yaml

kubectl create -f examples/guestbook/redis-master-service.yaml


vim examples/guestbook/redis-slave-deployment.yaml
vim examples/guestbook/frontend-deployment.yaml
vim examples/guestbook/all-in-one/redis-slave.yaml
vim examples/guestbook/all-in-one/frontend.yaml
env:
  - name: GET_HOSTS_FROM
    value: env

kubectl create -f examples/guestbook/all-in-one/redis-slave.yaml

vim examples/guestbook/all-in-one/frontend.yaml
spec:
  type: NodePort

kubectl create -f examples/guestbook/all-in-one/frontend.yaml


------------------------------------------

kubectl create -f examples/guestbook-go/redis-master-controller.json

kubectl create -f examples/guestbook-go/redis-master-service.json

kubectl create -f examples/guestbook-go/redis-slave-controller.json

kubectl create -f examples/guestbook-go/redis-slave-service.json

kubectl create -f examples/guestbook-go/guestbook-controller.json

kubectl create -f examples/guestbook-go/guestbook-service.json



kubectl delete -f examples/guestbook-go/redis-master-service.json

kubectl delete -f examples/guestbook-go/redis-slave-service.json

kubectl delete -f examples/guestbook-go/guestbook-service.json
