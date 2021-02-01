# dockerreg-cache
Docker registry as cache registry for kubernetes for dockerhub 

This is can be useful if you are hitting a limits on pull request 

Important for install must define a pv with name docker-repo-pv and one pvc with name docker-repo-pvc, no one yml is defined to leave this step free for your configuration

---
### Note
I've added the docker_cache_deployment_apps if you want to use docker cache as a normal deploy, this can be useful if you have a big enviroment, ofcourse you must use a pvc readwrite many as default (for this container) so de deploy is more faster than only one container.

---

## This deploy is a statefulsets or deployment apps and use a configmap for the configuration 

* The important config
inside configmap.yml you can modify the folder for docker registry or the docker registry that you want to cache

```yaml
filesystem:
        rootdirectory: /var/lib/registry ---> you can modify this with your best config, this is the folder location inside the container



proxy:
      remoteurl: https://registry-1.docker.io ---> you can modify the docker registry (now is a proxy for dockerhub)
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