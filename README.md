# eck-resources-with-helm-charts

If you want a solution where you can run only 4 commands and have your kubernetes observability (logs & metrics, dashboards ..) automatically set up, this guide is for you.
Here we will use helm to spin up Elastic Stack on ECK(Elastic on Kubernetes), with automatically Kubernetes observability.
We are going to run only 4 commands and we will have Elasticsearch, Kibana, Fleet & Elastic Agents (with System & Metrics of Kubernetes enabled).
Once you follow this guide, at the end you can access Kibana and quickly check your Kubernetes healthy, as the image below:

This page will give a generic way on how to set up ECK resources via helm. Keep in mind that you should adjust/add chart values that are relevant for your use case.

`stack/charts/elasticsearch/values.yml`: You should adjust this file to meet your use cases requirements, using this chart you can enable dedicated notes for: `master, data, data_hot, data_cold, data_frozen, ingest` nodes. If you don't want to use a dedicated node, a node will be created containing all the roles (default). If you want to create data dedicated nodes, make sure to also enable `master` dedicated nodes.

Before deploying Elasticsearch & Kibana make sure you deployed the ECK operator, the steps to do so in the following:
- `helm repo add elastic https://helm.elastic.co`
- `helm install elastic-operator elastic/eck-operator -n elastic-system --create-namespace`

Once, you have the operator up & running, you should clone this repo and either spin up the `stack` (which has dependencies Elasticsearch and Kibana) or you can choose to spin up only Elasticsearch (or only Kibana).

Let's assume you want to spin up the stack (Elasticsearch & Kibana), you should run the following:
- `helm install elastic-stack ./stack`

In case you want to deploy only Elasticsearch:
- `helm install <CHARTNAME> ./stack/charts/elasticsearch`

If you decide to spin up only Kibana, you should run:
- `helm install <CHARTNAME> ./stack/charts/kibana`

Done, with that you have Elasticsearch & Kibana up and running. Now we want to use Fleet and elastic agents to collect logs & metrics from our Kubernetes cluster where ECK is running. To do so, the `fleet-
server` chart has elastic-agent as a dependency.

To install that, run the following:
- `helm install <CHARTNAME> ./fleet-server`

Happy Helming and Observability!
