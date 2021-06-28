# dd-otel-tracing
Steps to perform this activity are as given below.

1. Create a datadog account.

2. To get the setup ready. From your kubernetes cluster setup run:
    a. helm repo add datadog https://helm.datadoghq.com
    b. helm repo add stable https://charts.helm.sh/stable
    c. helm repo update
    d. Downlaod the datadog.yaml file from: https://github.com/DataDog/helm-charts/blob/master/charts/datadog/values.yaml
    e. helm install <RELEASE_NAME> -f <DATADOG_YAML_FILE> --set datadog.site='datadoghq.com' --set datadog.apiKey=<DATADOG_API_KEY>
    f. git clone https://github.com/kuriouscoder/dd-otel-tracing

3. Deploy the application and otel-collector.
    a. Service account which gives otel-collector priveledge to read and watch cluster changes:
       kubectl apply -f service-account.yaml
    b. Deploy otel-config.yaml with your desired datadog api key:
       kubectl apply -f otel-config.yaml
    c. Deploy your application:
       kubectl apply -f microservices.yaml/deployment.yaml

4. Uninstall and deleting deployment.
   a. kubectl delete -f *.yaml
   b. helm uninstall <RELEASE_NAME>
