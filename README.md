# Setup de Cluster Kubernetes com Kind

Este guia descreve como configurar um cluster Kubernetes usando a ferramenta `kind` e como instalar o `kubectl`, a ferramenta de linha de comando para interagir com clusters Kubernetes.

## Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas:

- [Docker](https://docs.docker.com/get-docker/) (necessário para criar os containers que compõem o cluster Kubernetes)
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) (opcional, mas útil para clonar repositórios)

## Passo 1: Instalar o Kind

`kind` (Kubernetes IN Docker) é uma ferramenta para executar clusters Kubernetes locais usando containers Docker como "nós". 

### 1.1. Instalação no Linux

Para instalar o `kind`, execute o comando abaixo:

Passos:
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

## Passo 2: Para instalar o kubectl, execute os comandos abaixo:
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

## Passo 3: Criando seu primeiro cluster:
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
- role: worker

## Passo 4: Criando seu primeiro pod:
apiVersion: v1
kind: Pod
metadata:
  name: nginx-giropops
  labels:
    run: nginx-giropops
    app: giropops-strigus
spec:
  containers:
  - name: nginx-giropops
    image: nginx
    ports:
    - containerPort: 80
    resources: 
      limits: 
        memory: "450Mi"
        cpu: "500m"
      requests:
        memory: "440Mi"
        cpu: "300m"
  dnsPolicy: ClusterFirst
  restartPolicy: Always

