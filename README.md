# Valut with consul 용 Backup

## 시작
Hashicorp 사의 Vault 용 Docker 설명인 [Docker + Consul + Vault: A Practical Guide](https://www.marcolancini.it/2017/blog-vault/)에 나오는 [소스](https://github.com/marco-lancini/docker_vault) 중 [backup](https://github.com/marco-lancini/docker_vault/tree/master/backup) 참조하여 Vault with consul 용 backup 컨터에너를 미리 만들어 놓음

## 목적
VMWare의 Photon OS를 vSphere (ESXi) 에서 동작시키려 보면 docker-compose 의 yaml 안에 build 를 제대로 수행 못함. 따라서 해당 컨테이너를 만들어 놓기로 함

## Dockerfile
```sh
FROM golang

# Get Dependencies
RUN go get -v github.com/hashicorp/consul/api
RUN go get -v github.com/docopt/docopt-go

# Build consul-backup
RUN git clone https://github.com/kailunshi/consul-backup.git
RUN cd consul-backup && go build && cp consul-backup /bin/

# Initialize
RUN mkdir -p /backup
WORKDIR /backup
```

> [docker_consul_vault/backup/Dockerfile](https://github.com/mcchae/docker_consul_vault/blob/master/backup/Dockerfile) 참조

