
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


```yaml
stages:
	- build
	- test

A:
	stage: build

B:
	stage: test
```

the container of each stage will destroy immediately after complete

Artifacts is the output

`test`

`exit`
`exit 1`
⤷ ERROR: Job failed: exit code 1 