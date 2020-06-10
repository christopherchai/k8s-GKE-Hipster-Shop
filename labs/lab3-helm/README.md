# Install Dynatrace OneAgent Operator for Kubernetes via Helm
1. We'll start by installing Helm.
``` bash
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get-helm-3 > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```
Run 
``` bash
helm version
```
to make sure that Helm has been installed successfully.
![helm-version](https://github.com/christopherchai/k8s-GKE-Hipster-Shop/blob/master/assets/helm-version.JPG)
Note: Make sure that <b>/usr/local/bin</b> is added to <b>$PATH</b>, or Helm command cannot be run.

2. Obtain API token and PaaS token from Dynatrace.
- API token <br>
Create one from Settings -> Integration -> Dynatrace API
  - Enable Access problem and event feed, metrics, and topology toggle
  - Enable Write Configuration toggle (needed for Activegate setup for the next step)<br>
![API-Token](https://github.com/Dynatrace-APAC/Workshop-Kubernetes/blob/master/assets/api-token.png)

- PaaS token <br>
Create one from Settings -> Integration -> Platform as a Service
![PaaS-Token](https://github.com/Dynatrace-APAC/Workshop-Kubernetes/blob/master/assets/paas-token.png)



:arrow_up: [Back to TOC](/README.md) :arrow_left: [Prev](../lab2/README.md)   :arrow_right: [Next](../lab3/README.md)  


