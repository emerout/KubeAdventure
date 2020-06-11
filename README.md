# Kubernetes Adventure

----
## Comparaison des offres

* [Docker swarm](https://docs.docker.com/engine/swarm/):
  * Pb restart docker
  * Une migration PiCaaSso impliquerait une réécriture des plugins
* [Kubernetes](https://github.com/kubernetes/kubernetes)
* [Nomad](https://github.com/hashicorp/nomad)

----
## Kubernetes offre de valeurs
>Quels sont les problèmes résolus par Kubernetes ?

* Distribution des containers suivant une façon **logique** et **efficace** sur les nodes
  * Déploiement de conteneurs en tenant compte de la répartition de la charger (load)sur les différents serveurs (machines) du cluster.

* Augmenter / Diminuer le nombre de containers **rapidement**

* Garantir un service up & running dans le temps : Nb de conteneurs nécessaires sont présents et en cours de fonctionnement (running)

* Prendre en compte la gestion des des changements réseau sous-jacents

* Tout ceci suivant des règles/directives écrites en YAML

----
## Qu'est ce qu'un Cluster Kubernetes ?

* Un ensemble de machines appelées **Nodes** (phy. ou virt. machine) hébergeant des conteneurs
d'applications gérées par kubernetes
* Un cluster est composé au minimum d'un **worker node** et d'un **master node**
* Master Node
  * Gestion des worker nodes et des pods du cluster
  * Plusieurs master nodes afin d'assurer la haute disponibilité et les bascules (High availability & failover)
* Worker Node
  * Héberge les pods du cluster c-a-d les composants de l'application.

----
## Cluster Kubernetes : PODS

* C'est le plus petite unité déployable de Kubernetes 
* Un pod est un conteneur au minimum ( peu être plus)
* Les pods tournent sur les nodes de type "Worker" (containers et plus ...)
* Ce sont des conteneurs qui partagent la même stack réseau
* Les sont identifiés via  un label comme tout objet Kubernetes
> Exemple: 
     ------     -------
    |Node1  |  |Node2  |
     -------    -------
    |Pod1   |  | Pod3  |
    |Pod2   |  |       |
     -------    -------

Si Pod1, 2, 3 sont de la même application, on les appelle des réplicats

----
## Cluster Kubernetes : DEPLOYMENTS

----
## Comment démarrer un Cluster Kubernetes ?

* MiniKube
  * https://github.com/kubernetes/minikube
* Play with Docker
* RiCaaS: Las Vegas : Kind Kube in Docker
* k3d = k3s in Docker

----
## k3d

* k3d = k3s + docker 
* Doc : https://github.com/rancher/k3d
* Prérequis

> k3s
    
    curl -sfL https://get.k3s.io | sh -
    sudo systemctl status k3s
    kubectl cluster-info

> Installation

    curl -s https://raw.githubusercontent.com/rancher/k3d/master/install.sh | bash
    k3d create --api-port 6550 --publish 8081:80 --workers 2
    export KUBECONFIG="$(k3d get-kubeconfig --name='k3s-default')" 
    kubectl cluster-info
    kubectl get nodes
    kubectl get all --all-namespaces

