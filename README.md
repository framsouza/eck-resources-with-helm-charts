# eck-resources-with-helm-charts

This guide will guide you through how to spin up ECK resources via helm charts.

First thing, (we as Elastic) we provide helm charts to deploy ECK operator as per this [page](https://github.com/elastic/cloud-on-k8s/tree/master/deploy) however, we do not have anything specific on how to setup Elasticsearch & Kibana once you have the operator up and running. This page will give a generic way on how to set up both. Keep in mind that you should also adjust/add values that are relevant for your use case. 

Before deploying Elasticsearch & Kibana make sure you deployed the ECK operator, the steps to do so in the following:
- `helm repo add elastic https://helm.elastic.co`
- `helm install elastic-operator elastic/eck-operator -n elastic-system --create-namespace`

Once, you have the operator up & running, you should clone this repo and either spin up the stack (which will spin up Elasticsearch and Kibana) or you can choose to spin up only Elasticsearch (or Kibana).

Let's assume you want to spin up the stack, you should run the following:
- `helm install elastic-stack ./stack`

In case you want to deploy only Elasticsearch:
- `helm install <CHARTNAME> ./elasticsearch`
If you decide to spin up only Kibana, you should run:
- `helm install <CHARTNAME> ./kibana`

_NOTES_: If you are using data dedicated nodes, make sure to also enable the dedicated master nodes.
If you don't want to use dedicated nodes, what will be triggered is an elasticsearch container which contains all the roles (master,data,ml,transform,ingest)

Happy Helming!
