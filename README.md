## Perform distribute load testing on K8S environment by Locust


## Deploy a sample WEB application for load testing


```bash
$ cd kubernetes-config
$ kubectl create -f sample-webapp-controller.yaml
$ kubectl create -f kubectl create -f sample-webapp-service.yaml
```

## Configure Target URL for Locust Deployment

```Update the TARGET_URL for Locust master and Locust worker to match the service name in sample-webapp-service.yaml
    - name: TARGET_URL
      value: http://sample-webapp:8000
```

### Deploy locust-master

```bash
$ kubectl create -f configmap.yaml
$ kubectl create -f locust-master-controller.yaml
$ kubectl create -f locust-master-service.yaml
```

### Deploy locust-worker

Now deploy `locust-worker-controller`:

```bash
$ kubectl create -f locust-worker-controller.yaml
```

You may scale out the locust worker with the following command
```bash
$ kubectl scale deployment.v1.apps/locust-worker --replicas=10

```

## Access Locust WEB UI

Check the Locust-master's NodePort
```bash
kubectl get svc -l app=locust-master
```

Then access the Locust WEB UI by accessing http://{NodeIP}:{NodePort} on browser


## Execute Load Testing

Enter for `number of users to simulate` and `Hatch rate`, then click `Start swarming`

![locust-start-swarming](images/locust-start-swarming.jpg)

Output

![locust-dashboard](images/locust-dashboard.jpg)

## License

This code is Apache 2.0 licensed and more information can be found in `LICENSE`. For information on licenses for third party software and libraries, refer to the `docker-image/licenses` directory.
