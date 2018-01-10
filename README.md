# azkaban-kubernetes-osx
Run Azkaban Scheduler on Kubernetes for OSX

More about Azkaban Scheduler: https://azkaban.github.io/ (frequently used together with Hadoop)

# 1. Prerequisites: 
1. Install Docker for Mac (new version that has Kubernetes)
2. Enable Kubernetes in Docker UI

![Kubernetes Preferences in Docker for MAC](dockermackubernetespreferences.png)

# 2. Install Azkaban scheduler (from Terminal)
```
$ docker stack deploy azkaban -c azkaban/docker-compose.yml
```

## 2.1. Should expect something like this (might take a few minutes < 5)
```
Stack azkaban was created
Waiting for the stack to be stable and running...
 - Service azkweb has one container running
 - Service mysql has one container running
 - Service azkexec has one container running
Stack azkaban is stable and running
```

# 3. Open browser on http://localhost:8081
Use username and password: azkaban

## 3.1 Should get something like this in the browser

![Azkaban Scheduler on Mac in Browser](azkabanscheduler.png)



