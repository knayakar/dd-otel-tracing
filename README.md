# dd-otel-tracing
Steps to perform this activity are as given below.

Create a datadog account. To get the setup ready. From your kubernetes cluster setup run:
1. helm repo add datadog https://helm.datadoghq.com
2. helm repo add stable https://charts.helm.sh/stable
3. helm repo update
4. Downlaod the datadog.yaml file from: https://github.com/DataDog/helm-charts/blob/master/charts/datadog/values.yaml
5. helm install <RELEASE_NAME> -f <DATADOG_YAML_FILE> --set datadog.site='datadoghq.com' --set datadog.apiKey=<DATADOG_API_KEY>
6. git clone https://github.com/kuriouscoder/dd-otel-tracing

Deploy the application and otel-collector.
1. Service account which gives otel-collector priveledge to read and watch cluster changes:
   kubectl apply -f service-account.yaml
2. Deploy otel-config.yaml with your desired datadog api key:
   kubectl apply -f otel-config.yaml
3. Deploy your application:
   kubectl apply -f microservices.yaml/deployment.yaml

Uninstall and/or delete deployment.
1. kubectl delete -f *.yaml
2. helm uninstall <RELEASE_NAME>
