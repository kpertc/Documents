
![[GitLab-CI-Helloworld.png]]

[[YAML]]
```yml
test:
    script: echo "Hello World"
```


字节GitLab 需要配置 shared runner `tags: -shared`
```yml
test:
	script: echo "Hello World 1"
	tags:
	- shared
```

<br>

> Docker is a containerization platform and runtime and Kubernetes is a platform for running and managing containers from many container runtimes. by [Kubernetes vs. Docker](https://www.atlassian.com/microservices/microservices-architecture/kubernetes-vs-docker#:~:text=Kubernetes%20vs.-,Docker,CRI%20(Container%20Runtime%20Interface)).