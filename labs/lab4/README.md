# Setting up Hipster Shop

For our Hands-On, you will need to run <a href="https://github.com/GoogleCloudPlatform/microservices-demo">Hipster Shop</a> which is a Google sample application.

### 1. Run the Hipster Shop

```bash
wget -O- https://raw.githubusercontent.com/christopherchai/k8s-GKE-Hipster-Shop/master/deploy.sh | bash
```

Once deployed, you can locate the front-end endpoint from GCP (<b>Kubernetes Engine -> Services & Ingress</b>)

![JSON](https://github.com/christopherchai/k8s-GKE-Hipster-Shop/blob/master/assets/Picture10.png)

Once running, you can go to the exposed frontend-external IP to go to Hipster Shop.

![JSON](https://github.com/christopherchai/k8s-GKE-Hipster-Shop/blob/master/assets/hipstershop.png)

:arrow_up: [Back to TOC](/README.md) :arrow_left: [Prev](../lab3/README.md)   :arrow_right: [Next](../lab5/README.md)  

If required, use ```bash kubectl delete deploy -n hipster-shop --all ``` to delete all hipster-shop pods permanently.
