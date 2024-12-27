# Kubernetes ConfigMap

A **ConfigMap** is a Kubernetes resource used to store configuration data that can be consumed by other resources, such as pods, deployments, or services. It allows you to separate configuration from application code, making your applications more flexible and easier to manage.

## What is a ConfigMap?

A ConfigMap is an API object used to store non-sensitive configuration data in key-value pairs. It can be used to store configuration files, environment variables, command-line arguments, or any other configuration-related data that can be accessed by pods running in a Kubernetes cluster.

### Benefits of Using ConfigMap:

- **Decouple Configuration**: ConfigMap allows you to store configuration outside of the application, making it easier to update without modifying the application code.

- **Environment-Specific Configurations**: You can create different ConfigMaps for various environments (e.g., development, staging, production) and switch between them without changing the application.

- **Reuse Configuration**: The same ConfigMap can be reused by multiple resources, reducing duplication and ensuring consistency.

## Creating a ConfigMap

### 1. Create ConfigMap from Literal Key-Value Pairs
You can create a ConfigMap directly from literal values.

#### Example:

kubectl create configmap <configmap-name> --from-literal=<key>=<value> --from-literal=<key2>=<value2>
kubectl create configmap app-config --from-literal=app_mode=production --from-literal=debug=false

### 2. Create ConfigMap from file
You can create a ConfigMap from a file, where each line of the file becomes a key-value pair.

#### Example:

kubectl create configmap <configmap-name> --from-file=<file-name>
kubectl create configmap app-config --from-file=./config/settings.conf

### 3. Create ConfigMap from directory containing files
You can also create a ConfigMap from an entire directory, where each file in the directory becomes a key in the ConfigMap, and the file content becomes the value.

#### Example:

kubectl create configmap <configmap-name> --from-file=<directory-path>
kubectl create configmap app-config --from-file=./config/


### 4. Create ConfigMap by applying the YAML file
You can create a ConfigMap from yaml file.

#### Example:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  app_mode: production
  debug: "false"
  db_host: "localhost"
  db_port: "5432"
```

kubectl apply -f configmap.yaml

## Use a ConfigMap in application

Once a ConfigMap is created, it can be consumed by pods in various ways.

1. **Using ConfigMap as Environment Variables**
Inject ConfigMap data into a container as environment variables.

Example (Pod YAML):

apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: my-app-container
      image: my-app-image
      envFrom:
        - configMapRef:
            name: <configmap-name>

In this example, the environment variables from the ConfigMap named <configmap-name> will be made available to the container.

2. **Using Specific Key from a ConfigMap**
Reference a specific key in the ConfigMap and set it as an environment variable.

Example (Pod YAML):

apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: my-app-container
      image: my-app-image
      env:
        - name: APP_MODE
          valueFrom:
            configMapKeyRef:
              name: <configmap-name>
              key: app_mode

In this case, the app_mode value from the ConfigMap will be set as the environment variable APP_MODE in the container.

### 3. Deleting a ConfigMap
To delete a ConfigMap, use the kubectl delete command.

Example:
kubectl delete configmap <configmap-name>
