
## 简介

> gitlab、gitlab-runner、executor之间关系:
> Gitlab Runner 本身只提供与 Gitlab CI/CD 通信的能力，而真正执行流水线的是其实是Executors

## 安装（ubuntu环境下）

1. apt-get工具安装
	`apt-get install gitlib-runner`

2. 下载安装包安装
```bash
# Download the binary for your system
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64

# Give it permission to execute
sudo chmod +x /usr/local/bin/gitlab-runner

# Create a GitLab Runner user
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

# Install and run as a service
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start

# 可以查看到gitlab-runner的工作目录和默认用户等一系列相关信息
ps aux|grep gitlab-runner

# 如果不想以gitlab-runner用户安装：
# 先卸载
sudo gitlab-runner uninstall
#以root用户身份安装
gitlab-runner install --working-directory /home/gitlab-runner --user root
#重启服务
systemctl restart gitlab-runner.service
```

## 配置

- 安装目录 /home/gitlab-runner
- 配置目录 /etc/gitlab-runner

## 注册executor到Gitlab

```bash
# 可以在gitlab的group或project右侧菜单settings->ci/cd->runner中找到
# url一般是gitlab的地址
# TOKEN是project或group的标识
sudo gitlab-runner register 
```

- url : gitlab地址（ip:port）
- token， 有两种方式，一种对应组(改组下所有project共用)，一种是单个项目
	- group-runner：
	- project-runner
- shell

## Executor类型
- Shell
- SSH
- Docker
- K8s
- ...


## FAQ

### 权限不足报错
> Preparing environment00:00
> Running on zkcsdn...
> ERROR: Job failed: prepare environment: exit status 1.

```bash
rm .bashrc_logout
```




