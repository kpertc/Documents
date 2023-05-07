#IT #web-dev 

[[YAML]]
[[Docker-Kubernetes]]

### Architecture

GitLab Server 
- Stores the results
- Manage the pipelines and the associated jobs

GitLab Runner
- Executes the job

### Hello World

```yml
test:
    script: echo "Hello World"
```
![[GitLab-CI-Helloworld.png]]



字节GitLab 需要配置 shared runner `tags: -shared`
```yml
test:
	script: echo "Hello World 1"
	tags:
	- shared
```

image 镜像
安装系统



```yml
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