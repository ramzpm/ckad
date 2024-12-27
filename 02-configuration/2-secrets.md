# Kubernetes Secrets

In Kubernetes, **Secrets** are used to store sensitive information, such as passwords, tokens, SSH keys, and certificates. Secrets allow you to manage and securely store sensitive data separately from your application's code, making your deployments more secure.

### Benefits of Using Secrets:

- **Security**: Secrets are base64-encoded and can be encrypted at rest, making them more secure than plain-text environment variables or configuration files.

- **Avoid Hardcoding Sensitive Information**: By using Secrets, you can prevent sensitive data like passwords and tokens from being hardcoded into the application or stored in plain text.

- **Access Control**: Kubernetes provides fine-grained access control to Secrets, allowing only authorized pods or users to access them.

- **Seamless Integration**: Secrets can be used in environment variables, volumes, and other configurations without modifying the application code.

## Creating a Secret

### 1. Create a Secret from Literal Key-Value Pairs
You can create a Secret from literal key-value pairs using the `kubectl create secret` command.

#### Example:
```bash
kubectl create secret generic my-secret --from-literal=username=myuser --from-literal=password=mypassword
```

This creates a Secret named `my-secret` containing two key-value pairs: `username=myuser` and `password=mypassword`.

### 2. Create a Secret from a File
You can create a Secret from a file, where the file's contents become the value associated with a key.

#### Example:
```bash
kubectl create secret generic my-secret --from-file=ssh-key=./ssh-key.pem
```

This creates a Secret named `my-secret` with the key `ssh-key` and the contents of `ssh-key.pem` as the value.

### 3. Create a Secret from a Directory
You can also create a Secret from an entire directory, where each file in the directory becomes a key and the file's contents are stored as the values.

#### Example:
```bash
kubectl create secret generic my-secret --from-file=./config-directory
```

This creates a Secret where each file in the `config-directory` becomes a key in the Secret.

## Viewing a Secret

You can view the details of a Secret using the `kubectl get` command.

#### Example:
```bash
kubectl get secret my-secret -o yaml
```

This will display the Secret in YAML format. By default, the data is base64-encoded, so you will need to decode it if you want to view it in plain text.

### Decoding Secret Data:
You can decode base64-encoded data using the `base64` command-line utility.

```bash
echo "<base64-encoded-value>" | base64 --decode
```

## Using Secrets in Pods

Once a Secret is created, it can be consumed by pods in various ways, such as environment variables, volumes, or through specific Kubernetes resources like `envFrom` or `env`.

### 1. Using Secrets as Environment Variables
You can inject a Secret into a container as environment variables.

#### Example (Pod YAML):
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
  - name: my-container
    image: my-image
    env:
      - name: DB_USER
        valueFrom:
          secretKeyRef:
            name: my-secret
            key: username
      - name: DB_PASS
        valueFrom:
          secretKeyRef:
            name: my-secret
            key: password
```

In this example:
- **`DB_USER`** is an environment variable that gets its value from the `username` key of the `my-secret` Secret.
- **`DB_PASS`** is an environment variable that gets its value from the `password` key of the `my-secret` Secret.

### 2. Using Secrets as Files in Volumes
You can mount a Secret as a volume, where each key in the Secret becomes a file with the corresponding value.

#### Example (Pod YAML):
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: my-container
      image: my-image
      volumeMounts:
        - name: secret-volume
          mountPath: /etc/secrets
  volumes:
    - name: secret-volume
      secret:
        secretName: my-secret
```

In this example, the Secret `my-secret` is mounted into the `/etc/secrets` directory inside the container, where each key-value pair in the Secret becomes a file in the directory.

### 3. Using Secrets with Kubernetes Deployments
You can also use Secrets in Kubernetes **Deployment** resources in a similar way to how they are used in pods.

#### Example (Deployment YAML):
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: my-image
          envFrom:
            - secretRef:
                name: my-secret
```

In this example, the `envFrom` directive is used to inject all the key-value pairs from the `my-secret` Secret as environment variables into the container.

## Managing Secrets

### 1. Editing a Secret
You can edit an existing Secret using the `kubectl edit` command:

```bash
kubectl edit secret my-secret
```

This will open the Secret in your default text editor, allowing you to modify its contents.

### 2. Deleting a Secret
You can delete a Secret using the `kubectl delete` command:

```bash
kubectl delete secret my-secret
```

This will remove the specified Secret from the cluster.

## Secret Encryption

By default, Secrets are stored in etcd in **base64** encoded form, but this is not encryption. Kubernetes provides the option to encrypt Secrets at rest using encryption providers (like AES) in the Kubernetes API server configuration.

To enable encryption for Secrets, you need to modify the Kubernetes cluster’s encryption configuration.

## Example of a Secret YAML

Here is an example of a Secret defined in YAML format:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: bXl1c2Vy  # base64 encoded value of 'myuser'
  password: bXlwYXNzd29yZA==  # base64 encoded value of 'mypassword'
```

To create this Secret, you can save it in a file (e.g., `secret.yaml`) and run:

kubectl apply -f secret.yaml

