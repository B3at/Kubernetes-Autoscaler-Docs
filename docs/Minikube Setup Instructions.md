This is a Step by Step Guide to install minikube and the provided Demonstrator Test Environment. Download Links for the Files will be provided in the Future.

Downloading all components:
-
1. Get and install minikube from the Website: https://minikube.sigs.k8s.io/docs/start/
2. From the Demonstrator Pull/Download MongoDB, Data Processing, Data Provider and Device Communication
3. Get and install helm: https://helm.sh/docs/intro/install/
4. From our provided Files you need: gitlab-credentials.yaml, newCalibration-pvc.yaml, data-providerNew.yaml, device-communication.yaml, data-processing.yaml

Setup MongoDB:
-
1. `kubectl create namespace demonstrator`
2. `kubectl apply -f gitlab-credentials.yaml`
3. Apply all yaml files from the mongo-master folder
4. `kubectl get pods`
5. Now you can Port Forward the mongo-express to test if it works (`kubectl port-forward service/[mongo_express_something] PORT`)

Setup Persistent Volume Claims:
-
1. `minikube addons enable volumesnapshots`
2. `minikube addons enable csi-hostpaht-driver`
3. `kubectl apply -f newCalibration-pvc.yaml`

Setup Data Provider/Data Processing/Device Communication:
-
1. `kubectl apply -f data-providerNew.yaml`
2. `kubectl get pods -n demonstrator`
3. `kubectl logs pod/[data-provider-something] -f -n demonstrator` to Test (First time installation will load a while)
4. Repeat above steps for Data Processing and Device Communication

Setup RabbitMQ:
-
1. `helm repo add bitnami https://charts.bitnami.com/bitnami`
2. `helm install my-rabbit-rabbitmq --set auth.username=user,auth.password=k7cwXXdsPk,persistence.enabled=false bitnami/rabbitmq`

Start Services:
-
1. Wait for Device Communication and Data Provider to finish in the Logs
2. `kubectl get services -n demonstrator`
3. `minikube service [service-name] --url` for Device Communication and Data Provider