# Installation guide

{% hint style="info" %}
The installation guide details the installation on a cloud environment. Contact us at support@vectice.com for help on a custom installation.
{% endhint %}

## Deploy the monitoring stack

### Preparing the context

Add the repository prometheus-community to the helm collection:

```sh
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

Set up the CONTEXT, to make sure on which cluster the deployment will be done \
Example here on a GCP environment

```sh
CONTEXT='gke_my_test_project_us-west1_my-vectice-cluster'
TARGET_URL='https://monitoring-vectice.my-company.com'
```

Create the monitoring namespace

```sh
kubectl --context $CONTEXT create namespace monitoring
```

Generate the certificate, in order to add it to a secret, in the namespace, the key and cert filenames are examples

```sh
keypath='/tmp/vectice-monitoring-cert.key'
certpath='/tmp/vectice-monitoring-cert.crt'
openssl req -x509 -nodes -newkey rsa:2048 -days 3650 -keyout $keypath -out $certpath -subj '/CN=${TARGET_URL}'
kubectl --context $CONTEXT -n monitoring create secret tls monitoring-tls --key $keypath --cert $certpath
```

### Customize the deployment

Retrieve `values.yaml` file from [here](https://github.com/prometheus-community/helm-charts/blob/main/charts/kube-prometheus-stack/values.yaml) and then make it a copy to `myvaluesfile.yaml`\
Then, you can edit `myvaluesfile.yml`, following the instructions on the [customizing page](installation-guide.md#customize-the-deployment).

```sh
cp values.yaml myvaluesfile.yml
```

### Run the deployment

```sh
helm --kube-context $CONTEXT install -n monitoring prometh prometheus-community/kube-prometheus-stack -f myvaluesfile.yml
```

### Upgrade the monitoring stack

```sh
helm --kube-context $CONTEXT -n monitoring upgrade prometh prometheus-community/kube-prometheus-stack -f myvaluesfile.yml
```

### Undeploy the monitoring stack

{% hint style="info" %}
This will delete the monitoring stack installed
{% endhint %}

```sh
helm --kube-context $CONTEXT -n monitoring uninstall prometh
```

## Configuring Grafana

Once your application is up and running, a few things are necessary to make it easy to access and monitor.

First, grab the public IP address assigned to your application. Then, head over to your DNS provider and connect your domain name to that IP address. This will give your application a memorable web address you can easily share.

Next, customize your Grafana instance with some dashboards. These dashboards will help you visualize and understand how your application is performing.

{% hint style="info" %}
Vectice can provide you grafana dashboards templates on demand.
{% endhint %}

### Adding other datasources

If you're using Google Cloud Platform (GCP), you can set up GCP monitoring as a data source for even more insights. There's a handy guide [here](https://grafana.com/docs/grafana/latest/datasources/google-cloud-monitoring/) to walk you through the steps.

Ensure you have a service account with the proper permissions. You can call it "grafana-exporter" and permit it to view monitoring data (the "Monitoring Viewer" role). Then, create a JSON key and import it into Grafana. This will allow Grafana to access the monitoring data from GCP.

{% hint style="info" %}
If you want to personalize your Grafana experience, you can easily set your preferred dashboard as the default one you see when you log in. Just go to your user profile settings and make the switch."
{% endhint %}
