# Complex Example

In this example, we're going to deploy a service that just return all environment variables in the response. This is a
simple service that we can use to demonstrate how to deploy a service in Kubernetes.

## Application
The app is a simple ExpressJS app that returns all environment variables in the response.

```javascript
...

app.get('/', (req, res) => {
    res.send(process.env);
});

...
```

## Deployment
After a push on the master branch, this code build a docker image and let us deploy it to the Kubernetes cluster.

```yaml
k apply -f configmap.yaml -f deployment.yaml -f imagepullsecrets.yaml -f secret.yaml -f ingress.yaml -f service.yaml
```

