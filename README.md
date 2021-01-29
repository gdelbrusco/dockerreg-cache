# dockerreg-cache
Docker registry as cache registry for kubernetes

Important for install must define a pv with name docker-repo-pv and one pvc with name docker-repo-pvc, no one yml is defined to leave this step free for your configuration

## This deploy is a statefulsets and use a configmap for the configuration 

* The important config
inside configmap.yml you can modify the folder for docker registry 

```yaml
filesystem:
        rootdirectory: /var/lib/registry ---> you can modify this with your best config
```