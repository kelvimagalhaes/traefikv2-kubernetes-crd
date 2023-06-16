# Traefikv2-kubernetes-crd
Implementação Traefikv2 em cluster k8s através do provider CRD

[O Kubernetes](https://kubernetes.io/) (k8s) fornece a capacidade de os [Ingress Controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/) serem implantados para direcionar o tráfego para os serviços. Isso significa que os serviços podem ser expostos fora do cluster sem a necessidade de um novo balanceador de carga para cada um. Em vez disso, uma entrada pode ser usada para rotear o tráfego para serviços com base em regras de roteamento, por exemplo, nome do host, caminho, cabeçalhos, etc.

[Traefik](https://traefik.io/traefik/) é um Cloud Native Edge Router e proxy reverso que pode direcionar o tráfego entre serviços com base em regras de roteamento. O Traefik fornece um Ingress Controller que pode ser implantado em clusters Kubernetes para essas finalidades. Traefik introduziu uma definição de recurso personalizado (CRD) do Kubernetes para o  [Ingress Routes](https://doc.traefik.io/traefik/providers/kubernetes-crd/), que é a base da configuração neste repositório.

[homologacao.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/00-namespaces/homologacao.yaml)
[traefik.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/00-namespaces/traefik.yaml)
[account.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/01-crd/account.yaml)
account.yaml
definitions.yaml
rbac.yaml
role-binding.yaml
role.yaml
pv.yaml
pvc.yaml
secret-dashboard.yaml
middlewares.yaml
middlewares.yaml
configmap.yaml
services.yaml
deployment.yaml
ingressroute.yaml
