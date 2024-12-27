
# Kubernetes `args` and `cmd` Attributes

In Kubernetes, containers in a pod are specified using a `container` definition in the pod's YAML file. Each container has the ability to specify its command and arguments for how it should start. These are configured using the **`command`** and **`args`** attributes. Although these attributes are related, they serve different purposes in specifying how a container is executed.

## 1. `command` Attribute

The `command` attribute in Kubernetes specifies the **entrypoint** for the container. It defines the executable that should be run when the container starts. In Docker terminology, this is equivalent to the **`CMD`** instruction in a Dockerfile, but in Kubernetes, it overrides the Docker image's default entrypoint (if specified).

### Syntax:
```yaml
command: ["/path/to/executable", "param1", "param2"]
```

### Default Behavior:
- If you don't specify the `command` attribute, the default entrypoint from the Docker image (if set) will be used.

### Example:
If you have a container that needs to run a custom script as the entrypoint, you can specify it like this:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
  - name: my-container
    image: my-image
    command: ["/usr/bin/my-app"]
```

In this example, when the container starts, it will execute the `/usr/bin/my-app` executable.

## 2. `args` Attribute

The `args` attribute in Kubernetes specifies the **arguments** to pass to the entrypoint. This is analogous to the **`CMD`** instruction in a Dockerfile, which provides arguments to the command that is executed. If both `command` and `args` are defined, `command` acts as the entrypoint, and `args` are passed as arguments to the command.

### Syntax:
```yaml
args: ["arg1", "arg2"]
```

### Default Behavior:
- If the `args` attribute is not specified, the default arguments from the Docker image (if defined) will be used.

### Example:
In this example, the container is running the `nginx` web server, but we are passing custom arguments for the container startup:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
  - name: nginx-container
    image: nginx
    command: ["/usr/sbin/nginx"]
    args: ["-g", "daemon off;"]
```

In this case:
- The **`command`** specifies the entrypoint, `/usr/sbin/nginx`.
- The **`args`** specify the arguments passed to `nginx`: `-g daemon off;`.

## Overriding the Default Command and Arguments

You can override both the `command` and `args` in Kubernetes to tailor how your container starts. If no `command` is provided, Kubernetes will use the Docker image's default entrypoint, and if no `args` are provided, it will use the image’s default arguments.

### Example of Full Override:
You can override both the `command` and `args`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-custom-app
spec:
  containers:
  - name: my-container
    image: my-image
    command: ["/bin/sh"]
    args: ["-c", "echo Hello, Kubernetes! && sleep 3600"]
```

In this example:
- **`command`**: `/bin/sh` is the entrypoint (i.e., shell).
- **`args`**: `-c "echo Hello, Kubernetes! && sleep 3600"` tells the shell to execute a command that prints a message and then sleeps for an hour.

## How `command` and `args` Work Together

- **`command`** is the entrypoint and will execute the executable.
- **`args`** are the parameters or arguments passed to the executable.
  
If both `command` and `args` are specified:
- Kubernetes will use the specified **`command`** as the entrypoint, and it will pass the specified **`args`** as arguments to that command.
  
If only `args` are specified, Kubernetes will use the default `command` defined in the Docker image (if any).

### Example - Both `command` and `args` Specified:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-container
spec:
  containers:
  - name: my-container
    image: my-image
    command: ["/bin/my-app"]
    args: ["-arg1", "-arg2"]
```

In this case:
- **`command`** is `/bin/my-app` (the entrypoint).
- **`args`** are `-arg1` and `-arg2`, which are passed to `/bin/my-app`.

### Example - Only `args` Specified:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-container
spec:
  containers:
  - name: my-container
    image: my-image
    args: ["-arg1", "-arg2"]
```

In this case:
- Kubernetes will use the default **entrypoint** (from the image).
- **`args`** are passed to that default entrypoint.
