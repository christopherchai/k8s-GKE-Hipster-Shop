# Install Dynatrace OneAgent Operator for Kubernetes via Helm
<b>Note:</b> If you want to try Google Marketplace then skip this and go to next page.

We'll start by installing Helm.
``` bash
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get-helm-3 > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```
Run 
``` bash
helm version
```
to make sure that Helm v3 has been installed successfully.

<b>Note:</b> Make sure that <b>/usr/local/bin</b> is added to <b>$PATH</b>, or Helm command cannot be run.

Obtain API token and PaaS token from Dynatrace.
- API token <br>
Create one from Settings -> Integration -> Dynatrace API
  - Enable Access problem and event feed, metrics, and topology toggle
  - Enable Write Configuration toggle (needed for Activegate setup for the next step)<br>
![API-Token](https://github.com/christopherchai/k8s-GKE-Hipster-Shop/blob/master/assets/api-token.png)
- PaaS token <br>
Create one from Settings -> Integration -> Platform as a Service
![PaaS-Token](https://github.com/christopherchai/k8s-GKE-Hipster-Shop/blob/master/assets/paas-token.png)

Add Dynatrace OneAgent Helm repository
``` bash
helm repo add dynatrace https://raw.githubusercontent.com/Dynatrace/helm-charts/master/repos/stable
```

Create a Dynatrace namespace.
``` bash
kubectl create namespace dynatrace
```

Create a <b>values.yaml</b> file with the following content.
``` bash
platform: "kubernetes"
operator:
  image: ""
oneagent:
  name: "oneagent"
  apiUrl: "https://ENVIRONMENTID.live.dynatrace.com/api"
  image: ""
  args:
    - --set-app-log-content-access=true
  env:
    - name: ONEAGENT_ENABLE_VOLUME_STORAGE
      value: "true"
  nodeSelector: {}
  labels: {}
  skipCertCheck: false
  disableAgentUpdate: false
  enableIstio: false
  dnsPolicy: ""
  resources: {}
  waitReadySeconds: null
  priorityClassName: ""
  serviceAccountName: ""
  proxy: ""
  trustedCAs: ""
secret:
  apiToken: "DYNATRACE_API_TOKEN"
  paasToken: "PLATFORM_AS_A_SERVICE_TOKEN"
```
See <b>values.yaml</b> in this repo for reference. Using <b>values.yaml</b> you will be able to pass OneAgent arguments like HOST_GROUP and --set-network-zone=<your.network.zone> in args.

Install OneAgent Operator.
``` bash
helm install dynatrace-oneagent-operator dynatrace/dynatrace-oneagent-operator -n dynatrace --values values.yaml
```
If you encounter problem such as <b>Error: could not find tiller</b>, run
``` bash
helm init --wait
```

Cheatsheet:
``` bash
helm repo update
helm search repo dynatrace-oneagent-operator
helm upgrade dynatrace-oneagent-operator dynatrace/dynatrace-oneagent-operator -n dynatrace --reuse-values
helm uninstall dynatrace-oneagent-operator -n dynatrace
```

:arrow_up: [Back to TOC](/README.md) :arrow_left: [Prev](../lab2/README.md)   :arrow_right: [Next](../lab3/README.md)  


