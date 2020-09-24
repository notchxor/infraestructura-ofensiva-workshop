# INFRAESTRUCTURA OFENSIVA 
En este workshop vamos a ver como levantar un cluster kubernetes como Command and Control y distintos redirectors para realizar un red team engagement o un pentest.

El workshop esta pensado para usar un baremetal y distintas vps o instancias de AWS, sin embargo si desean probar algunos ejemplos de forma local van a necesitar docker, minikube/k3s y traefik.



# K3s
Para instalar k3s:

curl -sfL https://get.k3s.io | sh -

van a encontrar un kubeconfig en /etc/rancher/k3s/k3s.yaml, el script va a instalar k3s y otras tools como kubectl, k3s-kilall.sh, k3s-uninstall.sh
ex:
sudo kubectl get nodes

K3S_TOKEN es creado en /var/lib/rancher/k3s/server/node-token . Para instalarlo en worker nodes podemos pasarle K3S_URL junto al  K3S_TOKEN o K3S_CLUSTER_SECRET ex:

curl -sfL https://get.k3s.io | K3S_URL=https://myserver:6443 K3S_TOKEN=XXX sh -

# Docker
Para instalar docker

seteando los repos


    $ sudo apt-get update

    $ sudo apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg-agent \
        software-properties-common

    la GPG key de Docker:

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    Verific ala fingerprint 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88

    $ sudo apt-key fingerprint 0EBFCD88

    pub   rsa4096 2017-02-22 [SCEA]
          9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
    uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
    sub   rsa4096 2017-02-22 [S]

    $ sudo apt-get update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io
    $ sudo docker run hello-world

# Repositorios

vamos a usar 3 repositorios: 

https://github.com/notchxor/infraestructura-ofensiva-workshop  
https://github.com/notchxor/infraestructura-ofensiva-cluster  
https://github.com/notchxor/infraestructura-ofensiva-infra  



* workshop: este repo, voy a ir actualizandolo con mas informacion y con la presentacion post workshop
* cluster: kubespray para deployar un cluster a un servidor baremetal
* infra: todos los yaml para armar los c2 y playbooks de ansible para redirectors


