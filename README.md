# Projeto rotten-potatoes

### Sobre o projeto
O projeto rotten-potatoes é um projeto desenvolvido em Python. O projeto tem como objetivo ser um exemplo para a criação de ambiente com containers usando Python.

### Criação do cluster
k3d cluster create meucluster --agents 3 --servers 2 -p 80:30000@loadbalancer" -p "8080:31000@loadbalancer" -p "8282:32000@loadbalancer" -p "9090:31500@loadbalancer"

### Observação do inicio do cluster
Executar kubectl apply -f k8s -R

### Criação do Loki
helm upgrade --install loki grafana/loki-stack --namespace loki --values values-loki.yaml --create-namespace

### Comando para pegar o password do grafana, o username é admin
kubectl get secret --namespace loki loki-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

### Acesso das ferramentas
Prometheus: http://localhost:8080/
Alert Manager: http://localhost:8282/
Application: http://localhost/swagger
Grafana: http://localhost:9090/
Loki: Para acesso do promtail, terá que ser feito um port-forward de um dos pods, kubectl port-forward svc/loki 3100:3100 e então acessar http://localhost:3100/metrics
Promtail: Para acesso do promtail, terá que ser feito um port-forward de um dos pods, kubectl port-forward pod/NOME_POD 3101:3101 e então acessar http://localhost:3101




# Project rotten-potatoes

### About the project
The project rotten-potatoes is a project developed in Python. The project goal is to be a example to environment creation with containers using Python.

### Cluster creation
k3d cluster create meucluster --agents 3 --servers 2 -p 80:30000@loadbalancer" -p "8080:31000@loadbalancer" -p "8282:32000@loadbalancer" -p "9090:31500@loadbalancer"

### Cluster initialization
Execute kubectl apply -f k8s -R

### Creation of Loki
helm upgrade --install loki grafana/loki-stack --namespace loki --values values-loki.yaml

### Command for get the password for grafana, the username is admin
kubectl get secret --namespace loki loki-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

### Access features:
Prometheus: http://localhost:8080/
Alert Manager: http://localhost:8282/
Aplicação: http://localhost/swagger
Grafana: http://localhost:9090/
Loki: For access loki, you have to use port-forward, kubectl port-forward svc/loki 3101:3101 then access http://localhost:3100/metrics
Promtail: For access promtail, you have to use port-forward of one of the pods, kubectl port-forward pod/POD_NAME 3101:3101 then access http://localhost:3101