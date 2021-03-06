## gke-deploy prepare

Execute prepare phase and skip apply phase

### Synopsis

Prepare to deploy to GKE by generating modified Kubernetes resource configs. Skip apply.

- Modify Kubernetes config YAMLs to:
  - Set the digest of images that match the [--image|-i] flag, if provided.
  - Add app.kubernetes.io/name=[--app|-a] label, if provided.
  - Add app.kubernetes.io/version=[--version|-v] label, if provided.


```
gke-deploy prepare [flags]
```

### Examples

```
  # Prepare only.
  gke-deploy prepare -f configs -i gcr.io/my-project/my-app:1.0.0 -a my-app -v 1.0.0 -o modified -n my-namespace

  # Execute prepare and apply, with an intermediary step in between (e.g., manually check modified YAMLs)
  gke-deploy prepare -f configs -i gcr.io/my-project/my-app:1.0.0 -a my-app -v 1.0.0 -o modified -n my-namespace
  cat modified/*
  gke-deploy apply -f modified -c my-cluster -n my-namespace -c my-cluster -l us-east1-b  # Pass modified directory to -f
```

### Options

```
  -a, --app string         Application name of the Kubernetes deployment.
  -x, --expose int         Creates a Service resource that connects to a deployed resource using a selector that matches the label with key as 'app' and value of the image name's suffix specified by --image. The port provided will be used to expose the deployed resource (i.e., port and targetPort will be set to the value provided in this flag).
  -f, --filename string    Config file or directory of config files to use to create the Kubernetes resources (file or files in directory must end with ".yml" or ".yaml"). If this field is not provided, base configs will be created: Deployment with image provided by --image and HorizontalPodAutoscaler. The application's name will be inferred by the image name's suffix.
  -h, --help               help for prepare
  -i, --image string       Image to be deployed.
  -L, --label strings      Label(s) to add to Kubernetes resources (k1=v1). Labels can be set comma-delimited or as separate flags. If two or more labels with the same key are listed, the last one is used.
  -n, --namespace string   Namespace of GKE cluster to deploy to. (default "default")
  -o, --output string      Target directory to store created and hydrated Kubernetes resource configs. Created configs will be stored in "<output>/created" and hydrated configs will be stored in "<output>/hydrated". (default "./output")
  -V, --verbose            Prints underlying commands being called to stdout.
  -v, --version string     Version of the Kubernetes deployment.
```

### SEE ALSO

* [gke-deploy](gke-deploy.md)	 - Deploy to GKE

###### Auto generated by spf13/cobra on 19-Jul-2019
