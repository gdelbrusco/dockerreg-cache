# dockerreg-cache
Docker registry as cache registry for kubernetes

Important for install must define a pv with name docker-repo-pv and one pvc with name docker-repo-pvc, no one yml is defined to leave this step free for your configuration

## This deploy is a statefulsets and use a configmap for the configuration 

* The important config
inside configmap.yml you can modify the folder for docker registry 

```yaml
filesystem:
        rootdirectory: /var/lib/registry ---> you can modify this with your best config, this is the folder location inside the container
```


## Use the docker cache 
After deploy of the statefulsets you can config the docker on all worker machine and master that point to the localhost:33036


The good config is to use hostname instead the localhost

This is an example of daemon.json config under /etc/docker

```
{
        "registry-mirrors": ["http://localhost:33036"]
}

suggested config

{
        "registry-mirrors": ["http://node_hostname:33036"]
}


```