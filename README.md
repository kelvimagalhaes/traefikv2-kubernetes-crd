 # Traefikv2-kubernetes-crd
 
Implementação Traefikv2 em cluster k8s através do provider CRD :alien:

[O Kubernetes](https://kubernetes.io/) (k8s) fornece a capacidade de os [Ingress Controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/) serem implantados para direcionar o tráfego para os serviços. Isso significa que os serviços podem ser expostos fora do cluster sem a necessidade de um novo balanceador de carga para cada um. Em vez disso, uma entrada pode ser usada para rotear o tráfego para serviços com base em regras de roteamento, por exemplo, nome do host, caminho, cabeçalhos, etc.

[Traefik](https://traefik.io/traefik/) é um Cloud Native Edge Router e proxy reverso que pode direcionar o tráfego entre serviços com base em regras de roteamento. O Traefik fornece um Ingress Controller que pode ser implantado em clusters Kubernetes para essas finalidades. Traefik introduziu uma definição de recurso personalizado (CRD) do Kubernetes para o  [Ingress Routes](https://doc.traefik.io/traefik/providers/kubernetes-crd/), que é a base da configuração neste repositório.

- [homologacao.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/00-namespaces/homologacao.yaml) - Namespaces
- [traefik.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/00-namespaces/traefik.yaml) - Namespaces
- [account.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/01-crd/account.yaml) - ServiceAccount 
- [definitions.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/01-crd/definitions.yaml) - CRDs
- [rbac.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/01-crd/rbac.yaml) - Cluster Roles
- [role-binding.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/01-crd/role-binding.yaml) - Cluster Roles
- [role.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/01-crd/role.yaml) - Cluster Roles
- [pv.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/02-volumes/pv.yaml) - (Opcional), volume criado do tipo hostPath, especificando caminho do certificado 
- [pvc.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/02-volumes/pvc.yaml) - (Opcional), mas é usuado para que o tráfego seja confiável, pois cria um volume persistente na máquina host que é usado para armazenar os certificados
- [secret-dashboard.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/03-secrets/secret-dashboard.yaml) - (Opcional), mas é necessário se usar a middlewares do tipo basicAuth para autenticar na página de dashboard do traefik.
--------------------------------
  :speaking_head:  **OBS: Se observar os 2 (dois) arquivos estão com as Middlewares de página de erros personalizada sendo roteados pelo serviço chamado "manutenção". Também a ipWhiteList impedindo a rede fictícia "10.10.0.0/22" de acessar determinado serviço conforme a necessidade de cada ambiente. Por último foi criado o redirecionamento automático para https através da middleware "redirectscheme", tomei a iniciativa de deixar a configuração de ingressroute para fazer gerência dessa função, sendo assim elas estão junto no final dos arquivos middlewares.yaml** :shipit:
- [middlewares.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/04-middlewares/namespaces/traefik/middlewares.yaml) - Middlewares criadas no namespace "traefik"
- [middlewares.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/04-middlewares/namespaces/homologacao/middlewares.yaml) - Middlewares criadas no namespace "homologacao"
-------------------------------- 
- [configmap.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/05-traefik/configmap.yaml) - Usado para armazenar a configuração dinâmica através do arquivo traefik.toml
- [services.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/05-traefik/services.yaml) - Expõe as portas do contêiner para traefik
- [deployment.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/05-traefik/deployment.yaml) - Configuração do pod Traefik com os pontos de montagens associado para cada volume persistente se integrar com certificado SSL e configuração do tipo dinâmica && File.
- [ingressroute.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/05-traefik/ingressroute.yaml) - Usado para expor da dashboard do Traefik externamente e proteger usando a middleware basicAuth.
-------------------------------- 
Serviço de manutenção, caso queira uma página de erro personalizada;
- [deployment.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/06-manutencao/deployment.yaml) - Configuração do Pod de manutenção, caso queira colocar uma página de erro html personalizada
- [service.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/06-manutencao/services.yaml) - Expõe as portas do container manutenção
- [ingressroute.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/06-manutencao/ingressroute.yaml) - Usado para criar a rota do serviço
- [pv.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/06-manutencao/volumes/pv.yaml) - Local de armazenamento do arquivo html
- [pvc.yaml](https://github.com/kelvimagalhaes/traefikv2-kubernetes-crd/blob/main/06-manutencao/volumes/pvc.yaml) - Cria um volume persistente na máquina host "manutenção"

