--Arquitetura de Kubernetes: control plane
Gerenciamento de clusters do Kubernetes é realizado por meio de um conjunto de componentes que formam o plano de
controle (control plane). Esses componentes são responsáveis por manter o estado desejado do cluster, tomar decisões de
agendamento, gerenciar a comunicação entre os nós e garantir a disponibilidade dos serviços. Os principais componentes
do control plane incluem:

- api server - (POD) -> é o componente central do control plane, responsável por expor a API do Kubernetes e servir como
  ponto de
  entrada para todas as operações do cluster. Ele é responsável por autenticar e autorizar solicitações, validar e
  processar objetos do Kubernetes, e manter o estado desejado do cluster. Ele também é responsável por
  armazenar o estado do cluster no etcd, que é um banco de dados chave-valor distribuído usado para armazenar a
  configuração e o estado do cluster.
- etcd - (Banco de dados) -> é um banco de dados chave-valor distribuído usado para armazenar a configuração e o estado do
  cluster. Ele é
  projetado para ser altamente disponível e consistente, garantindo que o estado do cluster seja sempre preciso e
  atualizado. O etcd é implementado em Go e é usado pelo API server para armazenar o estado desejado do cluster, bem como
  para armazenar informações sobre os nós, pods, serviços e outros recursos do Kubernetes.
- cloud controller - (POD) -> responsável por interagir com provedores de nuvem para gerenciar recursos de infraestrutura,
  como
  balanceadores de carga, volumes de armazenamento e instâncias de máquinas virtuais. Ele é projetado para ser modular,
  permitindo que o Kubernetes suporte uma variedade de provedores de nuvem, como AWS, Azure e Google Cloud.
- controller manager - (POD) -> é responsável por executar os controladores que gerenciam o estado do cluster. Ele inclui
  controladores para gerenciar nós, pods, serviços, endpoints e outros recursos do Kubernetes. O controller manager é
  projetado para ser altamente disponível, permitindo que o Kubernetes continue a operar mesmo se
  um controlador falhar.
- scheduler - (POD) -> é responsável por agendar os pods nos nós de trabalho com base em uma série de critérios, como
  recursos
  disponíveis, afinidade e anti-afinidade, e políticas de tolerância. Projetado para
  ser altamente eficiente, permitindo que o Kubernetes agende rapidamente os pods em clusters de grande escala.

--Arquitetura de Kubernetes: data plane
O data plane do Kubernetes é composto pelos nós de trabalho (worker nodes) que executam as cargas de trabalho (pods) e
são gerenciados pelo control plane. Cada nó de trabalho possui um agente chamado kubelet, que é responsável por garantir
que os contêineres estejam em execução e saudáveis. O data plane também inclui o kube-proxy, que é responsável por
gerenciar a rede e o balanceamento de carga entre os pods. Os principais componentes do data plane incluem:

- worker nodes -> são os nós de trabalho que executam as cargas de trabalho (pods) e são gerenciados pelo control plane.
  Cada nó de trabalho é responsável por executar os pods agendados pelo scheduler e garantir que eles estejam em execução
  e saudáveis. Os nós de trabalho podem ser máquinas físicas ou virtuais e são projetados para ser altamente escaláveis,
  permitindo que o Kubernetes gerencie clusters de grande escala com milhares de nós.
- kubelet -> é o agente que roda em cada nó de trabalho e é responsável por garantir que os contêineres estejam em
  execução e saudáveis. Ele se comunica com o API server para receber instruções sobre quais pods devem ser executados no
  nó e para relatar o status dos pods em execução. Garantindo que os pods sejam mantidos em execução mesmo em caso de
  falhas temporárias.
- kube-proxy -> é responsável por gerenciar a rede e o balanceamento de carga entre os pods. Ele implementa as
  regras de
  rede para garantir que os pods possam se comunicar entre si e com o mundo externo. Permite que o Kubernetes gerencie a
  rede de forma eficaz mesmo em clusters de grande escala.

--Kind
É uma ferramenta de código aberto que permite criar clusters Kubernetes locais usando contêineres Docker. Ele é
projetado para ser fácil de usar e é ideal para desenvolvimento, teste e aprendizado do Kubernetes. O Kind permite que
os desenvolvedores criem clusters Kubernetes em suas máquinas locais sem a necessidade de configurar uma infraestrutura
de nuvem ou virtualização complexa. Ele é amplamente utilizado para testes de integração, desenvolvimento de aplicativos
e aprendizado do Kubernetes, proporcionando uma maneira rápida e eficiente de criar clusters Kubernetes para fins de
desenvolvimento e teste.

--kind comandos
`kind create cluster` -> cria um cluster Kubernetes local usando contêineres Docker.
`kind create cluster --name <nome-do-cluster>` -> cria um cluster Kubernetes local com um nome específico usando
contêineres Docker.
`kind create cluster --config <caminho-para-configuração>` -> cria um cluster Kubernetes local usando um arquivo de
configuração personalizado.
`kind create cluster --image <imagem-do-node>` -> cria um cluster Kubernetes local usando uma imagem personalizada para os
nós.
`kind create cluster --wait` -> cria um cluster Kubernetes local e aguarda até que o cluster esteja pronto antes de
retornar.
`kind create cluster --kubeconfig <caminho-para-kubeconfig>` -> cria um cluster Kubernetes local e salva o arquivo
kubeconfig em um caminho específico.
`kind create cluster --retain` -> cria um cluster Kubernetes local e mantém os contêineres Docker mesmo após a exclusão do
cluster.
`kind create cluster --nodes <número-de-nós>` -> cria um cluster Kubernetes local com um número específico de nós.
`kind create cluster --control-plane <número-de-nós-de-control-plane>` -> cria um cluster Kubernetes local com um número
específico de nós de control plane.
`kind delete cluster` -> exclui um cluster Kubernetes local criado com o Kind.
`kind get clusters` -> lista os clusters Kubernetes locais criados com o Kind.
`kind get nodes` -> lista os nós de trabalho (worker nodes) em um cluster Kubernetes local criado com o Kind.
`kind get pods` -> lista os pods em um cluster Kubernetes local criado com o Kind.
`kind get services` -> lista os serviços em um cluster Kubernetes local criado com o Kind.
`kind get deployments` -> lista os deployments em um cluster Kubernetes local criado com o Kind.
`kind get replicasets` -> lista os ReplicaSets em um cluster Kubernetes local criado com o Kind.
`kind get statefulsets` -> lista os StatefulSets em um cluster Kubernetes local criado com o Kind.
`kind get daemonsets` -> lista os DaemonSets em um cluster Kubernetes local criado com o Kind.
`kind get ingress` -> lista os Ingresses em um cluster Kubernetes local criado com o Kind.
`kind get configmaps` -> lista os ConfigMaps em um cluster Kubernetes local criado com o Kind.
`kind get secrets` -> lista os Secrets em um cluster Kubernetes local criado com o Kind.
`kind get namespaces` -> lista os namespaces em um cluster Kubernetes local criado com o Kind.
`kind get events` -> lista os eventos em um cluster Kubernetes local criado com o Kind.

Ex de comando para criar um cluster Kubernetes local usando o Kind com um arquivo de configuração personalizado e salvar
o:

```bash
kind create cluster --config config.yaml --name comunidade-devops --kubeconfig config
```

Ex de arquivo de configuração personalizado para criar um cluster Kubernetes local com um nó de control plane e dois nós
de trabalho:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
    kubeadmConfigPatches:
      - |
        kind: InitConfiguration
        nodeRegistration:
          kubeletExtraArgs:
            node-labels: "ingress-ready=true"
    extraPortMappings:
      - containerPort: 80
        hostPort: 80
        listenAddress: "0.0.0.0"
        protocol: TCP
      - containerPort: 443
        hostPort: 443
        listenAddress: "0.0.0.0"
        protocol: TCP
      - containerPort: 8080
        hostPort: 8080
        listenAddress: "0.0.0.0"
        protocol: TCP
  - role: worker
  - role: worker
```

--Kubectl
Kubectl é a ferramenta de linha de comando oficial para interagir com clusters Kubernetes. Ele permite que os usuários
gerenciem recursos do Kubernetes, como pods, serviços, deployments e outros objetos, por meio de comandos simples. O
Kubectl é uma parte essencial do ecossistema Kubernetes e é amplamente utilizado por desenvolvedores, administradores de
sistemas e engenheiros de DevOps para gerenciar e operar clusters Kubernetes. Ele suporta uma ampla variedade de
comandos para criar, atualizar, excluir e visualizar recursos do Kubernetes, tornando-o uma ferramenta poderosa para a
administração de clusters Kubernetes.

--Comandos kubectl
`kubectl get` -> lista os recursos do Kubernetes, como pods, serviços, deployments e outros objetos.
`kubectl describe` -> exibe detalhes sobre um recurso específico do Kubernetes, como um pod ou serviço.
`kubectl create` -> cria um recurso do Kubernetes a partir de um arquivo de configuração ou diretamente na linha de
comando.
`kubectl apply` -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de configuração, criando ou
atualizando o recurso conforme necessário.
`kubectl delete` -> exclui um recurso do Kubernetes, como um pod, serviço ou deployment.
`kubectl logs` -> exibe os logs de um pod específico, permitindo que os usuários monitorem o comportamento dos contêineres
em execução.
`kubectl exec` -> executa um comando em um contêiner em execução dentro de um pod, permitindo que os usuários interajam
diretamente com os contêineres para depuração ou administração.
`kubectl port-forward` -> encaminha uma porta local para um pod específico, permitindo que os usuários acessem serviços em
execução dentro do cluster Kubernetes a partir de suas máquinas locais.
`kubectl scale` -> escala um recurso do Kubernetes, como um deployment ou replicaset, aumentando ou diminuindo o número de
réplicas conforme necessário.
`kubectl rollout` -> gerencia o processo de implantação de um recurso do Kubernetes, permitindo que os usuários monitorem
o status da implantação, pausem ou retomem a implantação, e revertam para uma versão anterior se necessário.
`kubectl top` -> exibe o uso de recursos, como CPU e memória, para pods ou nós em um cluster Kubernetes, permitindo que os
usuários monitorem o desempenho e a utilização dos recursos em seus clusters Kubernetes.
`kubectl config` -> gerencia os arquivos de configuração do Kubernetes, permitindo que os usuários configurem e alternem
entre diferentes clusters Kubernetes, usuários e contextos.
`kubectl apply -f <arquivo.yaml>` -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de
configuração YAML, criando ou atualizando o recurso conforme necessário.
`kubectl get pods` -> lista os pods em um cluster Kubernetes, mostrando informações como nome, status, idade e outros
detalhes relevantes.
`kubectl describe pod <nome-do-pod>` -> exibe detalhes sobre um pod específico, incluindo informações sobre os contêineres
em execução, eventos relacionados e outros detalhes importantes para a depuração e administração do pod.
`kubectl logs <nome-do-pod>` -> exibe os logs de um pod específico, permitindo que os usuários monitorem o comportamento
dos contêineres em execução e identifiquem possíveis problemas ou erros.
`kubectl exec -it <nome-do-pod> -- <comando>` -> executa um comando interativo em um contêiner em execução dentro de um
pod, permitindo que os usuários interajam diretamente com os contêineres para depuração ou administração.
`kubectl port-forward <nome-do-pod> <porta-local>:<porta-do-pod>` -> encaminha uma porta local para um pod específico,
permitindo que os usuários acessem serviços em execução dentro do cluster Kubernetes a partir de suas máquinas locais.
`kubectl scale deployment <nome-do-deployment> --replicas=<número-de-réplicas>` -> escala um deployment específico,
aumentando ou diminuindo o número de réplicas conforme necessário para atender à demanda ou otimizar o uso de recursos.
`kubectl rollout status deployment <nome-do-deployment>` -> monitora o status da implantação de um deployment específico,
permitindo que os usuários verifiquem se a implantação foi bem-sucedida, se há falhas ou se a implantação está em
andamento.
`kubectl config use-context <nome-do-contexto>` -> alterna para um contexto específico em um arquivo de configuração do
Kubernetes, permitindo que os usuários gerenciem e operem diferentes clusters Kubernetes, usuários e contextos de forma
eficiente.    
`kubectl config view` -> exibe o conteúdo do arquivo de configuração do Kubernetes, mostrando informações sobre os
clusters, usuários e contextos configurados, permitindo que os usuários verifiquem e gerenciem suas configurações de
acesso ao Kubernetes.
`kubectl config get-contexts` -> lista os contextos disponíveis em um arquivo de configuração do Kubernetes, mostrando
informações sobre os clusters, usuários e contextos configurados, permitindo que os usuários escolham o contexto
apropriado para suas operações no Kubernetes.
`kubectl config current-context` -> exibe o contexto atual em uso em um arquivo de configuração do Kubernetes, permitindo
que os usuários verifiquem qual cluster, usuário e contexto estão ativos para suas operações no Kubernetes.
`kubectl api-resources` -> lista os tipos de recursos disponíveis na API do Kubernetes, mostrando informações sobre os recursos
suportados, suas versões e se eles são recursos de namespace ou de cluster, permitindo que os usuários entendam os recursos disponíveis para gerenciamento e
operação em seus clusters Kubernetes.
`kubectl get pod -n kube-system <pod-name>` -> exibe detalhes sobre um pod específico no namespace kube-system, que é o namespace onde os componentes do control
plane do Kubernetes geralmente são executados. Este comando é útil para verificar o status e os logs dos pods do control plane, permitindo que os usuários
monitorem a saúde e o desempenho dos componentes essenciais do Kubernetes em seus clusters.
`kubectl get pod -n kube-system <pod-name> -o` -> exibe detalhes sobre um pod específico no namespace kube-system em um formato de saída específico, como JSON
ou
YAML, permitindo que os usuários obtenham informações detalhadas sobre o pod e seus recursos associados para depuração e administração avançada no Kubernetes.
`kubectl get pod -n kube-system <pod-name> -o json` -> exibe detalhes sobre um pod específico no namespace kube-system em formato JSON, permitindo que os
usuários
obtenham informações estruturadas e detalhadas sobre o pod e seus recursos associados para depuração e administração avançada no Kubernetes.
`kubectl get pod -n kube-system <pod-name> -o yaml` -> exibe detalhes sobre um pod específico no namespace kube-system em formato YAML, permitindo que os
usuários
obtenham informações estruturadas e detalhadas sobre o pod e seus recursos associados para depuração e administração avançada no Kubernetes.
`kubectl get pod -n kube-system <pod-name> -o wide` -> exibe detalhes sobre um pod específico no namespace kube-system em um formato de saída mais amplo,
mostrando informações adicionais como o nó onde o pod está em execução, o endereço IP do pod e outras informações relevantes para monitoramento e administração
no Kubernetes.
`kubectl get pod -n kube-system <pod-name> -o =jsonpath='{.status.phase}'` -> exibe o status de um pod específico no namespace kube-system usando uma expressão
jsonpath para extrair apenas o valor do campo status.phase, permitindo que os usuários obtenham informações específicas sobre o estado do pod de forma eficiente
no Kubernetes.
`kubectl get pod -Aowide` -> lista todos os pods em todos os namespaces com informações adicionais, mostrando detalhes como o namespace, o nome do pod, o
status,
a idade, o nó onde o pod está em execução e outras informações relevantes para monitoramento e administração em um cluster Kubernetes.
`kubectl get pod -n kube-system --show-labels` -> lista os pods no namespace kube-system e exibe as labels associadas a cada pod, permitindo que os usuários
vejam
as labels usadas para organizar e selecionar os pods no Kubernetes, o que é útil para gerenciamento e administração eficiente dos recursos do cluster.
`kubectl get pod -n kube-system --show-labels <label-selector>` -> lista os pods no namespace kube-system que correspondem a um seletor de labels específico,
permitindo que os usuários filtrem os pods com base em suas labels para gerenciamento e administração eficiente dos recursos do cluster Kubernetes.
`kubectl get -n kube-system etcd-comunidade-devops-control-plane -oyaml` -> exibe detalhes sobre o pod etcd-comunidade-devops-control-plane no namespace
kube-system em formato YAML, permitindo que os usuários obtenham informações estruturadas e detalhadas sobre o pod etcd e seus recursos associados para
depuração e administração avançada no Kubernetes.
`kubectl delete pod <pod-name>` -> exclui um pod específico do cluster Kubernetes, permitindo que os usuários removam pods que não são mais necessários ou que
estão causando problemas no cluster.
`kubectl delete pod <pod-name> -n <namespace>` -> exclui um pod específico de um namespace específico no cluster Kubernetes, permitindo que os usuários removam
pods de forma mais granular e organizada dentro do cluster.
`kubectl delete deployment <deployment-name>` -> exclui um deployment específico do cluster Kubernetes, permitindo que os usuários removam deployments que não
são
mais necessários ou que estão causando problemas no cluster.
`kubectl delete service <service-name>` -> exclui um serviço específico do cluster Kubernetes, permitindo que os usuários removam serviços que não são mais
necessários ou que estão causando problemas no cluster.

--Configurando o kubectl para acessar um cluster Kubernetes local criado com o Kind
Para configurar o kubectl para acessar um cluster Kubernetes local criado com o Kind, siga os passos abaixo:
opção 1:

1. Crie um cluster Kubernetes local usando o Kind, se ainda não tiver feito isso. Você pode usar o comando
   `kind create cluster --config config.yaml --name comunidade-devops --kubeconfig config` para criar um cluster local.
2. Após a criação do cluster, o kind gera um arquivo admin.config que contém as informações de acesso ao cluster. Para acessar esse arquivo você precisa acessar
   o contêiner do nó de control plane usando o comando `docker exec -it <nome-do-contêiner> bash`, onde `<nome-do-contêiner>` é o nome do contêiner do nó de
   control plane criado pelo Kind.
3. Dentro do contêiner do nó de control plane, você pode encontrar o arquivo admin.config no diretório `/etc/kubernetes/`. Acesse o conteudo do arquivo
   admin.config usando o comando `nano admin.config` e copie o conteúdo do arquivo.
4. Após isso se estiver usando windows, acesse a pasta `C:\Users\SeuUsuario\.kube\`, verifique se existe o arquivo `config`, caso ele não exista crie e cole o
   conteúdo
   do arquivo admin.config copiado anteriormente nesse novo arquivo `config`.
5. Se ao rodar o comando `kubectl get pod -A` e der o erro dial tcp: `lookup comunidade-devops-control-plane: no such host` significa que o kubectl não consegue
   resolver o DNS do nome do control-plane do seu cluster kind. Isso acontece porque o **contexto do kubeconfig aponta para um cluster que não existe mais** (ou
   foi
   recriado com outro nome). O kind usa o nome do cluster para montar o hostname interno, e o kubeconfig ficou com a referência antiga. Voce pode ver como esta
   o seu kubeconfig usando o comando `kubectl config view --minify`, provavelmente você vai ver algo assim
   `server: https://comunidade-devops-control-plane:6443`. O kind no Linux usa a rede interna do Docker para resolver esse hostname, mas no **Windows isso não
   funciona diretamente** — o kubectl roda fora do WSL/Docker e não enxerga a rede interna dos containers. Para corrigir isso, você
   precisa reexportar o kubeconfig
   com o comando `kind export kubeconfig --name comunidade-devops` e depois confira se mudou `kubectl config view --minify`, deve mostrar:
   server: https://127.0.0.1:PORTA

opção 2:

1. Crie um cluster Kubernetes local usando o Kind, se ainda não tiver feito isso. Você pode usar o comando `kind create cluster` para criar um cluster local.
2. Após a criação do cluster, o Kind gera um arquivo kubeconfig que contém as informações de acesso ao cluster. Por padrão, o Kind salva esse arquivo em um
   local temporário, mas você pode especificar um caminho personalizado usando a opção `--kubeconfig` ao criar o cluster.
3. Para configurar o kubectl para usar o arquivo kubeconfig gerado pelo Kind, você pode usar o comando `kubectl config use-context` para alternar para o
   contexto do cluster criado pelo Kind. O nome do contexto geralmente segue o formato `kind-<nome-do-cluster>`, onde `<nome-do-cluster>` é o nome que você
   especificou ao criar o cluster.
4. Verifique se o kubectl está configurado corretamente para acessar o cluster Kubernetes local criado com o Kind usando o comando
   `kubectl config current-context`. Ele deve exibir o nome do contexto do cluster criado pelo Kind, indicando que o kubectl está configurado para acessar o
   cluster local.
5. Agora você pode usar o kubectl para gerenciar e operar o cluster Kubernetes local criado com o Kind, executando comandos como `kubectl get pods`,
   `kubectl apply -f <arquivo.yaml>`, e outros comandos do kubectl para interagir com os recursos do Kubernetes em seu cluster local. Certifique-se de que o
   cluster esteja em execução e que o kubectl esteja configurado corretamente para acessar o cluster local para garantir que suas operações sejam bem-sucedidas.

--Fazer o merge do arquivo kubeconfig
Se você tiver vários clusters Kubernetes e quiser combinar os arquivos kubeconfig para gerenciar todos eles com o kubectl, você pode usar o comando `kubectl config
view --merge --flatten > merged-kubeconfig.yaml` para criar um arquivo kubeconfig combinado. Este comando irá mesclar os arquivos kubeconfig existentes e criar
um novo arquivo chamado `merged-kubeconfig.yaml` que contém as informações de acesso para todos os clusters Kubernetes configurados. Depois de criar o arquivo
kubeconfig combinado, você pode configurar o kubectl para usar esse arquivo usando o comando `export KUBECONFIG=merged-kubeconfig.yaml` no Linux ou
`set KUBECONFIG=merged-kubeconfig.yaml` no Windows. Isso permitirá que você gerencie todos os seus clusters Kubernetes usando um único arquivo kubeconfig,
facilitando a administração e operação de múltiplos clusters Kubernetes com o kubectl. Certifique-se de que o arquivo kubeconfig combinado contenha as
informações corretas de acesso para cada cluster Kubernetes para garantir que suas operações sejam bem-sucedidas.
Um ponto que deve ser observado é que o cluster e user do contexto e name em users devem ser únicos, caso contrário, o kubectl pode ter problemas para resolver
os contextos corretamente. Se houver conflitos de nomes, você pode editar o arquivo kubeconfig combinado para renomear os clusters, usuários e contextos de
forma única, garantindo que o kubectl possa resolver os contextos corretamente ao gerenciar múltiplos clusters Kubernetes. Certifique-se de que cada cluster,
usuário e contexto tenha um nome exclusivo no arquivo kubeconfig combinado para evitar conflitos e garantir que o kubectl funcione corretamente ao acessar os
diferentes clusters Kubernetes configurados. Após configurar o kubectl para usar o arquivo kubeconfig combinado, você pode verificar os contextos disponíveis
usando o comando `kubectl config get-contexts` e alternar entre eles usando o comando `kubectl config use-context <nome-do-contexto>`, permitindo que você
gerencie facilmente múltiplos clusters Kubernetes com o kubectl.

--etcd: Configurando o etcdctl
O etcdctl é a ferramenta de linha de comando para interagir com o banco de dados etcd, que é usado pelo Kubernetes para armazenar a configuração e o estado do
cluster. Para configurar o etcdctl para acessar o cluster Kubernetes local criado com o Kind, siga os passos abaixo:

1. Acesse o contêiner do nó de control plane do cluster Kubernetes local criado com o Kind usando o comando `docker exec -it <nome-do-contêiner> bash`, onde
   `<nome-do-contêiner>` é o nome do contêiner do nó de control plane criado pelo Kind.
2. Dentro do contêiner do nó de control plane, você pode encontrar o arquivo de configuração do etcdctl em `/etc/kubernetes/pki/etcd/`. Este arquivo é usado
   para autenticar o etcdctl com o cluster Kubernetes e acessar o banco de dados etcd.
3. Para configurar o etcdctl, você precisa exportar as variáveis de ambiente necessárias para autenticar o etcdctl com o cluster Kubernetes. Você pode fazer
   isso usando os seguintes comandos dentro do contêiner do nó de control plane:

```bash
export ETCDCTL_API=3
export ETCDCTL_CACERT=/etc/kubernetes/pki/etcd/ca.crt
export ETCDCTL_CERT=/etc/kubernetes/pki/etcd/server.crt
export ETCDCTL_KEY=/etc/kubernetes/pki/etcd/server.key
```

4. Após exportar as variáveis de ambiente, você pode usar o etcdctl para interagir com o banco de dados etcd do cluster Kubernetes local criado com o Kind. Por
   exemplo, você pode usar o comando `etcdctl get / --prefix` para listar todas as chaves e valores armazenados no etcd, ou usar outros comandos do etcdctl para
   gerenciar o banco de dados etcd conforme necessário.
5. Certifique-se de que o cluster Kubernetes local criado com o Kind esteja em execução e que as variáveis de ambiente estejam configuradas corretamente para
   garantir que o etcdctl possa acessar o banco de dados etcd do cluster Kubernetes local criado com o Kind. Isso permitirá que você gerencie e opere o banco de
   dados etcd do cluster Kubernetes local criado com o Kind usando o etcdctl de forma eficiente e segura. Lembre-se de que o acesso ao etcd deve ser feito com
   cuidado, pois ele contém informações sensíveis sobre o cluster Kubernetes, e o uso inadequado do etcdctl pode levar a problemas de segurança ou perda de
   dados. Certifique-se de entender os comandos do etcdctl e suas implicações antes de usar a ferramenta para gerenciar o banco de dados etcd do cluster
   Kubernetes local criado com o Kind.
6. Para facilitar pode ser criado um etcdctl.env com as variáveis de ambiente necessárias para o etcdctl, e depois exportar essas variáveis usando o comando
   `source etcdctl.env` dentro do
   contêiner do nó de control plane. Isso permitirá que você configure o etcdctl de forma mais conveniente e reutilizável, evitando a necessidade de exportar as
   variáveis de ambiente manualmente toda vez que precisar usar o etcdctl para interagir com o banco de dados etcd do cluster Kubernetes local criado com o
   Kind. O conteúdo do arquivo etcdctl.env deve ser o seguinte:

```bash
cat <<EOF > etcdctl.env
export ETCDCTL_API=3
export ETCDCTL_CACERT=/etc/kubernetes/pki/etcd/ca.crt
export ETCDCTL_CERT=/etc/kubernetes/pki/etcd/server.crt
export ETCDCTL_KEY=/etc/kubernetes/pki/etcd/server.key
EOF
```

--etcd:Backup e snapshot do etcd
O etcd é um banco de dados chave-valor distribuído usado pelo Kubernetes para armazenar a configuração e o estado do cluster. É importante fazer backup do etcd
regularmente para garantir que você possa recuperar o estado do cluster em caso de falhas ou perda de dados. O etcdctl oferece comandos para criar snapshots do
banco de dados etcd, que podem ser usados como backups. Para criar um snapshot do etcd usando o etcdctl, você pode usar o comando
`etcdctl snapshot save <caminho-do-arquivo>`, onde `<caminho-do-arquivo>`(/var/lib/etcd) é o caminho onde você deseja salvar o arquivo de snapshot. Este comando
irá criar um
snapshot do banco de dados etcd e salvá-lo no local especificado. Certifique-se de armazenar os snapshots em um local seguro e acessível para garantir que você
possa recuperá-los quando necessário. Além disso, é recomendável criar uma estratégia de backup regular para o etcd, garantindo que você tenha cópias
atualizadas do estado do cluster Kubernetes para recuperação em caso de falhas ou perda de dados. Para restaurar um snapshot do etcd usando o etcdctl, você pode
usar o comando `etcdctl snapshot restore <caminho-do-arquivo>`, onde `<caminho-do-arquivo>` é o caminho para o arquivo de snapshot que você deseja restaurar.
Este comando irá restaurar o banco de dados etcd a partir do snapshot especificado, permitindo que você recupere o estado do cluster Kubernetes a partir do
backup. Certifique-se de entender as implicações de restaurar um snapshot do etcd, pois isso pode afetar o estado do cluster Kubernetes e deve ser feito com
cuidado para evitar perda de dados ou interrupção do cluster. Sempre teste a restauração de snapshots do etcd em um ambiente de teste antes de aplicá-la em um
cluster de produção para garantir que o processo funcione corretamente e que você possa recuperar o estado do cluster Kubernetes com sucesso usando o etcdctl.

--Comandos etcdctl
`etcdctl get / --prefix` -> lista todas as chaves e valores armazenados no banco de dados etcd, mostrando informações sobre a configuração e o estado do cluster
Kubernetes.
`etcdctl put <chave> <valor>` -> adiciona ou atualiza uma chave e valor no banco de dados etcd, permitindo que os usuários gerenciem a configuração e o estado
do
cluster Kubernetes de forma eficiente usando o etcdctl.
`etcdctl del <chave>` -> exclui uma chave do banco de dados etcd, permitindo que os usuários removam informações desnecessárias ou obsoletas do cluster
Kubernetes
usando o etcdctl.
`etcdctl member list` -> lista os membros do cluster etcd, mostrando informações sobre os nós do cluster etcd, suas IDs, status e outras informações relevantes
para monitoramento e administração do cluster etcd usando o etcdctl.
`etcdctl member add <nome-do-membro> --peer-urls=<url-do-peer>` -> adiciona um novo membro ao cluster etcd, permitindo que os usuários expandam o cluster etcd
adicionando novos nós usando o etcdctl.
`etcdctl member remove <id-do-membro>` -> remove um membro do cluster etcd, permitindo que os usuários reduzam o cluster etcd removendo nós usando o etcdctl.
`etcdctl snapshot save <caminho-do-arquivo>` -> salva um snapshot do banco de dados etcd em um arquivo, permitindo que os usuários criem backups do estado do
cluster Kubernetes usando o etcdctl.
`etcdctl snapshot restore <caminho-do-arquivo>` -> restaura um snapshot do banco de dados etcd a partir de um arquivo, permitindo que os usuários recuperem o
estado do cluster Kubernetes a partir de um backup usando o etcdctl.
`etcdctl endpoint health` -> verifica a saúde dos endpoints do cluster etcd, mostrando informações sobre o status dos nós do cluster etcd e permitindo que os
usuários monitorem a saúde do cluster etcd usando o etcdctl.
`etcdctl endpoint status` -> exibe o status dos endpoints do cluster etcd, mostrando informações detalhadas sobre os nós do cluster etcd, como a versão do etcd,
o
número de membros, o tempo de resposta e outras informações relevantes para monitoramento e administração do cluster etcd usando o etcdctl.
`etcdctl endpoint status --write-out=table` -> exibe o status dos endpoints do cluster etcd em formato de tabela, mostrando informações detalhadas sobre os nós
do
cluster etcd de forma organizada e fácil de ler para monitoramento e administração do cluster etcd usando o etcdctl.
`etcdctl endpoint status --write-out=fields` -> exibe o status dos endpoints do cluster etcd em formato de campos, mostrando informações detalhadas sobre os nós
do cluster etcd em um formato mais compacto e fácil de processar para monitoramento e administração do cluster etcd usando o etcdctl.
`etcdctl endpoint status --write-out=json` -> exibe o status dos endpoints do cluster etcd em formato JSON, mostrando informações detalhadas sobre os nós do
cluster etcd em um formato estruturado e fácil de processar para monitoramento e administração do cluster etcd usando o etcdctl.
`etcdctl endpoint status --write-out=yaml` -> exibe o status dos endpoints do cluster etcd em formato YAML, mostrando informações detalhadas sobre os nós do
cluster etcd em um formato estruturado e fácil de ler para monitoramento e administração do cluster etcd usando o etcdctl.

--YAML com kubernetes
O Kubernetes usa arquivos de configuração em formato YAML para definir e gerenciar recursos do cluster, como pods, serviços, deployments e outros objetos. Esses
arquivos YAML são usados para criar, atualizar e excluir recursos do Kubernetes de forma declarativa, permitindo que os usuários definam o estado desejado dos
recursos e apliquem essas configurações ao cluster Kubernetes usando o comando `kubectl apply -f <arquivo.yaml>`. Os arquivos YAML do Kubernetes seguem uma
estrutura específica, com campos como `apiVersion`, `kind`, `metadata` e `spec` para definir os recursos do Kubernetes de forma clara e organizada. O uso de
arquivos YAML no Kubernetes permite que os usuários gerenciem seus recursos de forma eficiente e consistente, facilitando a administração e operação de clusters
Kubernetes em ambientes de desenvolvimento, teste e produção. É importante entender a estrutura e os campos dos arquivos YAML do Kubernetes para criar e
gerenciar recursos do Kubernetes de forma eficaz usando o kubectl e garantir que suas configurações sejam aplicadas corretamente ao cluster Kubernetes.
Certifique-se de validar seus arquivos YAML usando ferramentas como `kubectl apply --dry-run=client -f <arquivo.yaml>` para verificar se eles estão corretos
antes de aplicá-los ao cluster Kubernetes, evitando erros de configuração e garantindo que seus recursos sejam criados ou atualizados com sucesso no cluster
Kubernetes.

Exemplo de arquivo YAML para criar um deployment do Kubernetes:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

--Namespace o que é e para que serve
No Kubernetes, um namespace é uma forma de organizar e isolar recursos dentro de um cluster. Ele permite que você crie múltiplos ambientes lógicos dentro do
mesmo cluster, cada um com seus próprios recursos, como pods, serviços e deployments. Os namespaces são úteis para separar diferentes equipes,projetos ou
ambientes (como desenvolvimento, teste e produção) dentro do mesmo cluster Kubernetes. Eles também ajudam a evitar conflitos de nomes entre recursos, permitindo
que você tenha recursos com o mesmo nome em diferentes namespaces. Além disso, os namespaces podem ser usados para aplicar políticas de segurança e controle de
acesso específicas para cada namespace, garantindo que os recursos sejam gerenciados de forma segura e eficiente dentro do cluster Kubernetes.

--Comandos relacionados a namespaces
`kubectl create namespace <nome-do-namespace>` -> cria um novo namespace no cluster Kubernetes, permitindo que os usuários organizem e isolem recursos dentro do
cluster Kubernetes usando namespaces.
`kubectl get namespaces` -> lista os namespaces disponíveis no cluster Kubernetes, mostrando informações sobre cada namespace, como nome, status e outras
informações relevantes para monitoramento e administração do cluster Kubernetes usando namespaces.
`kubectl delete namespace <nome-do-namespace>` -> exclui um namespace do cluster Kubernetes, removendo todos os recursos associados a esse namespace, permitindo
que os usuários limpem recursos desnecessários ou obsoletos do cluster Kubernetes usando namespaces.
`kubectl get pods -n <nome-do-namespace>` -> lista os pods em um namespace específico, mostrando informações como nome, status, idade e outros detalhes
relevantes
para monitoramento e administração dos recursos dentro do namespace usando o kubectl.
`kubectl apply -f <arquivo.yaml> -n <nome-do-namespace>` -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de configuração YAML dentro
de
um namespace específico, criando ou atualizando o recurso conforme necessário, permitindo que os usuários gerenciem recursos de forma eficiente dentro do
namespace usando o kubectl.
`kubectl config set-context --current --namespace=<nome-do-namespace>` -> define o namespace padrão para o contexto atual do kubectl, permitindo que os usuários
trabalhem com um namespace específico sem precisar especificar o namespace em cada comando do kubectl, facilitando a administração e operação de recursos dentro
do namespace usando o kubectl. Certifique-se de que o namespace especificado exista no cluster Kubernetes para evitar erros ao usar o kubectl com o namespace
configurado.

--namespaces padrões
O Kubernetes vem com alguns namespaces pré-definidos que são usados para diferentes propósitos dentro do cluster. Os namespaces padrão incluem:

- `default`: Este é o namespace padrão onde os recursos são criados se nenhum namespace for especificado. Ele é usado para recursos que não se encaixam em
  outros
  namespaces ou para recursos de teste e desenvolvimento.
- `kube-system`: Este namespace é usado para os componentes do control plane do Kubernetes, como o kube-apiserver, kube-controller-manager, kube-scheduler e
  outros
  componentes essenciais do cluster Kubernetes. Ele é reservado para os recursos do sistema e não deve ser usado para recursos de usuário.
- `kube-public`: Este namespace é usado para recursos que devem ser acessíveis publicamente, como ConfigMaps ou Secrets que precisam ser compartilhados entre
  diferentes namespaces. Ele é de leitura pública e pode ser acessado por qualquer usuário do cluster Kubernetes.
- `kube-node-lease`: Este namespace é usado para armazenar informações sobre os nós do cluster Kubernetes, como o status dos nós e as informações de lease. Ele
  é usado para monitorar a saúde dos nós e garantir que eles estejam funcionando corretamente dentro do cluster Kubernetes.
- `local-path-storage`: Este namespace é usado para os recursos relacionados ao local-path-storage, que é um provisionador de armazenamento local para o
  Kubernetes. Ele é usado para fornecer armazenamento persistente para os pods dentro do cluster Kubernetes usando o armazenamento local do nó.

--Pods
No Kubernetes, um pod é a menor unidade de implantação e execução. Ele representa um grupo de um ou mais contêineres que compartilham o mesmo ambiente de
execução, como rede, armazenamento e recursos de computação. Os pods são usados para executar aplicativos e serviços dentro do cluster Kubernetes, e cada pod é
atribuído a um nó do cluster para execução. Os pods são efêmeros, o que significa que eles podem ser criados,atualizados e excluídos dinamicamente pelo
Kubernetes com base na demanda e nas necessidades do cluster. Os pods são gerenciados por controladores, como deployments, statefulsets e daemonsets, que
garantem que o número desejado de réplicas de pods esteja sempre em execução e que os pods sejam reiniciados ou substituídos em caso de falhas. Os pods também
podem ser expostos a outros recursos do Kubernetes, como serviços, para permitir a comunicação entre os pods e outros recursos dentro do cluster Kubernetes.
Normalmente cada pod contem um container com uma aplicação, mas é possível ter mais de um container em um pod, normalmente é criado um sidecar para realizar
tarefas auxiliares para a aplicação principal, como monitoramento, logging ou proxy reverso. Os pods são uma parte fundamental do Kubernetes e são usados para
executar e gerenciar aplicativos e serviços dentro do cluster Kubernetes de forma eficiente e escalável.

As vezes é necessário acessar o terminal de um container em execução dentro de um pod para depuração ou administração. Para isso, você pode usar o comando
`kubectl exec -it <nome-do-pod> -- <comando>`, onde `<nome-do-pod>` é o nome do pod que contém o container que você deseja acessar, e `<comando>` é o comando
que você deseja executar dentro do container. Por exemplo, se você quiser acessar um terminal interativo dentro do container, pode usar o comando
`kubectl exec -it <nome-do-pod> -- sh` para iniciar um shell dentro do container. Isso permitirá que você interaja diretamente com o container para depuração ou
administração usando o kubectl. Certifique-se de que o pod esteja em execução e que o container que você deseja acessar esteja saudável para garantir que o
comando `kubectl exec` funcione corretamente e que você possa acessar o terminal do container com sucesso.
Uma forma de manter o pod sempre em execução para acessar o terminal interativo é criar um pod com um contêiner que execute um comando de longa duração, como
`sleep infinity`. Isso garantirá que o pod permaneça em execução indefinidamente, permitindo que você acesse o terminal interativo do contêiner a qualquer
momento usando o comando `kubectl exec -it <nome-do-pod> -- sh` ou outro comando de shell. Certifique-se de que o pod esteja configurado corretamente para
garantir que ele permaneça em execução e que você possa acessar o terminal do contêiner de forma eficiente para depuração ou administração usando o kubectl.
Abaixo esta uma forma de criar um pod com um contêiner que execute o comando `sleep infinity` para manter o pod em execução:

```yamlapiVersion: v1
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: terraform-demo
  name: terraform-demo
spec:
  containers:
    - image: hashicorp/terraform:latest
      name: terraform-demo
      resources: { }
      command:
        - "sleep"
        - "infinity"
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

--Comandos relacionados a pods
`kubectl run <nome-do-pod> --image=<imagem-do-container>` -> cria um novo pod com um contêiner específico, permitindo que os usuários implantem aplicativos e
serviços dentro do cluster Kubernetes usando o kubectl.
`kubectl run --image=<imagem-do-container> --rm -it sh <nome-do-pod>` -> cria um novo pod com um contêiner específico e inicia um terminal interativo dentro do
contêiner, permitindo que os usuários interajam diretamente com o contêiner para depuração ou administração usando o kubectl. O pod será removido
automaticamente após a sessão interativa ser encerrada.
`kubectl run --image=<imagem-do-container> <nome-do-pod> --dry-run -oyaml` -> gera um arquivo YAML de configuração para um pod com um contêiner
específico, permitindo que os usuários criem um arquivo de configuração para o pod e personalizem suas configurações antes de aplicá-lo ao cluster Kubernetes
usando o kubectl.
`kubectl run --image=<imagem-do-container> <nome-do-pod> --dry-run -oyaml > <arquivo.yaml>` -> gera um arquivo YAML de configuração para um pod com um contêiner
específico e salva o arquivo em um local especificado, permitindo que os usuários criem um arquivo de configuração para o pod e personalizem suas configurações
antes de aplicá-lo ao cluster Kubernetes usando o kubectl.
`kubectl apply -f <arquivo.yaml>` -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de configuração YAML, criando ou atualizando o
recurso
conforme necessário, permitindo que os usuários gerenciem recursos do Kubernetes de forma eficiente usando o kubectl.
`kubectl get pods` -> lista os pods em um cluster Kubernetes, mostrando informações como nome, status, idade e outros detalhes relevantes para monitoramento e
administração dos recursos do cluster Kubernetes usando o kubectl.
`kubectl get pods -w` -> lista os pods em um cluster Kubernetes e continua monitorando as mudanças em tempo real, mostrando informações como nome, status, idade
e
outros detalhes relevantes para monitoramento e administração dos recursos do cluster Kubernetes usando o kubectl.
`kubectl describe pod <nome-do-pod>` -> exibe detalhes sobre um pod específico, incluindo informações sobre os contêineres em execução, eventos relacionados e
outros detalhes importantes para a depuração e administração do pod usando o kubectl.
`kubectl logs <nome-do-pod>` -> exibe os logs de um pod específico, permitindo que os usuários monitorem o comportamento dos contêineres em execução e
identifiquem possíveis problemas ou erros usando o kubectl.
`kubectl exec -it <nome-do-pod> -- <comando>` -> executa um comando interativo em um contêiner em execução dentro de um pod, permitindo que os usuários
interajam
diretamente com os contêineres para depuração ou administração usando o kubectl.
`kubectl port-forward <nome-do-pod> <porta-local>:<porta-do-pod>` -> encaminha uma porta local para um pod específico, permitindo que os usuários acessem
serviços
em execução dentro do cluster Kubernetes a partir de suas máquinas locais usando o kubectl.
`kubectl delete pod <nome-do-pod>` -> exclui um pod específico do cluster Kubernetes, permitindo que os usuários removam pods que não são mais necessários ou
que
estão causando problemas no cluster usando o kubectl.
`kubectl get pods -n <nome-do-namespace>` -> lista os pods em um namespace específico, mostrando informações como nome, status, idade e outros detalhes
relevantes
para monitoramento e administração dos recursos dentro do namespace usando o kubectl.
`kubectl describe pod <nome-do-pod> -n <nome-do-namespace>` -> exibe detalhes sobre um pod específico em um namespace específico, incluindo informações sobre os
contêineres em execução, eventos relacionados e outros detalhes importantes para a depuração e administração do pod dentro do namespace usando o kubectl.
`kubectl logs <nome-do-pod> -n <nome-do-namespace>` -> exibe os logs de um pod específico em um namespace específico, permitindo que os usuários monitorem o
comportamento dos contêineres em execução e identifiquem possíveis problemas ou erros dentro do namespace usando o kubectl.
`kubectl exec -it <nome-do-pod> -n <nome-do-namespace> -- <comando>` -> executa um comando interativo em um contêiner em execução dentro de um pod específico em
um namespace específico, permitindo que os usuários interajam diretamente com os contêineres para depuração ou administração dentro do namespace usando o
kubectl.
`kubectl port-forward <nome-do-pod> -n <nome-do-namespace> <porta-local>:<porta-do-pod>` -> encaminha uma porta local para um pod específico em um namespace
específico, permitindo que os usuários acessem serviços em execução dentro do cluster Kubernetes a partir de suas máquinas locais usando o kubectl, mesmo quando
os pods estão organizados em namespaces diferentes.
`kubectl delete pod <nome-do-pod> -n <nome-do-namespace>` -> exclui um pod específico de um namespace específico do cluster Kubernetes, permitindo que os
usuários
removam pods de forma mais granular e organizada dentro do cluster usando o kubectl, garantindo que os recursos sejam gerenciados de forma eficiente dentro dos
namespaces do cluster Kubernetes. Certifique-se de que o namespace especificado exista no cluster Kubernetes para evitar erros ao usar o kubectl com o
namespaceconfigurado.

--Init containers
Os init containers são contêineres especiais que são executados antes dos contêineres principais em um pod do Kubernetes. Eles são usados para realizar tarefas
de inicialização, como configuração,verificação de dependências ou preparação do ambiente antes que os contêineres principais sejam iniciados. Os init
containers são definidos na seção `initContainers` do arquivo de configuração do pod e são executados em ordem, um após o outro. Cada init container deve ser
concluído com sucesso antes que o próximo seja iniciado, e os contêineres principais só serão iniciados após a conclusão de todos os init containers. Os init
containers são úteis para garantir que o ambiente do pod esteja configurado corretamente antes que os contêineres principais sejam executados, permitindo que os
usuários realizem tarefas de inicialização de forma eficiente e organizada dentro do cluster Kubernetes usando o kubectl.
Abaixo está um exemplo de configuração de init containers em um arquivo YAML para um pod do Kubernetes:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-cd
  namespace: default
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
  initContainers:
    - name: waitfordns
      image: busybox:latest
      command: [ 'sh', '-c', 'until nslookup mymysql.default.svc.cluster.local; do echo waiting for dns...; sleep 2; done;' ]
```

O nginx-cd é o contêiner principal do pod, que executa a imagem do nginx e expõe a porta 80. O init container waitfordns é executado antes do contêiner
principal e usa a imagem do busybox para executar um comando que verifica se o serviço de banco de dados MySQL (mymysql) está disponível no cluster Kubernetes.
O init container aguarda até que o serviço de banco de dados esteja disponível antes de permitir que o contêiner principal seja iniciado, garantindo que o
ambiente do pod esteja configurado corretamente para a aplicação nginx funcionar corretamente.

--Multi-container pods
Os multi-container pods são pods do Kubernetes que contêm mais de um contêiner. Eles são usados para executar aplicativos que exigem a colaboração de múltiplos
contêineres, como uma aplicação principal e um sidecar para realizar tarefas auxiliares, como monitoramento, logging ou proxy reverso. Os multi-container pods
são definidos na seção `containers` do arquivo de configuração do pod, onde cada contêiner é especificado com seu nome, imagem e outras configurações
relevantes. Os contêineres dentro de um multi-container pod compartilham o mesmo ambiente de execução, como rede, armazenamento e recursos de computação,
permitindo que eles se comuniquem e colaborem de forma eficiente dentro do pod. Os multi-container pods são úteis para executar aplicativos complexos que exigem
a colaboração de múltiplos contêineres, permitindo que os usuários criem e gerenciem recursos de forma eficiente dentro do cluster Kubernetes usando o kubectl.
Abaixo está um exemplo de configuração de multi-container pods em um arquivo YAML para um pod do Kubernetes:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: multicontainerpod
  name: multicontainerpod
spec:
  containers:
    - image: httpd
      name: httpd
    - image: alpine:latest
      name: debug
      command: [ "sleep", "infinity" ]
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

O multi-container pod chamado multicontainerpod contém dois contêineres: o contêiner httpd, que executa a imagem do servidor web Apache HTTP, e o contêiner
debug,que executa a imagem do Alpine Linux e tem um comando de longa duração para manter o pod em execução. Os contêineres dentro do multi-container pod
compartilham o mesmo ambiente de execução, permitindo que eles se comuniquem e colaborem de forma eficiente dentro do pod. O contêiner httpd pode servir
conteúdo web, enquanto o contêiner debug pode ser usado para depuração ou administração do pod usando o comando `kubectl exec` para acessar o terminal do
contêiner debug. Caso seja removido o command do conteiner debug, o pod irá entrar em crashloop, pois o
contêiner debug não terá um comando de longa duração para manter o pod em execução, e o Kubernetes tentará reiniciar o pod repetidamente, resultando em um ciclo
de falhas (crashloop) para o contêiner debug.

--Static pods
Os static pods são um tipo especial de pod no Kubernetes que são gerenciados diretamente pelo kubelet em um nó específico do cluster, em vez de serem
gerenciados pelo control plane do Kubernetes. Eles são usados para executar componentes essenciais do cluster Kubernetes, como o kube-apiserver,
kube-controller-manager e kube-scheduler, que são necessários para o funcionamento do cluster Kubernetes. Os static pods são definidos em arquivos de
configuração YAML que são colocados em um diretório específico no nó, geralmente `/etc/kubernetes/manifests/`. O kubelet monitora esse diretório e cria os
static pods com base nos arquivos de configuração encontrados lá. Os static pods são úteis para garantir que os componentes essenciais do cluster Kubernetes
estejam sempre em execução, mesmo que o control plane do Kubernetes esteja indisponível, permitindo que o cluster Kubernetes continue funcionando de forma
resiliente. Lembre-se de que os static pods são gerenciados diretamente pelo kubelet e não são controlados pelo
control plane do Kubernetes, portanto, eles não são afetados por falhas ou indisponibilidade do control plane, garantindo que os componentes essenciais do
cluster Kubernetes estejam sempre em execução para manter o cluster Kubernetes funcionando de forma resiliente.
Abaixo está um exemplo de configuração de static pods em um arquivo YAML para um pod do Kubernetes:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: multicontainerpod
  name: multicontainerpod
spec:
  containers:
    - image: httpd
      name: httpd
    - image: alpine:latest
      name: debug
      command: [ "sleep", "infinity" ]
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

--Lifecycle dos pods
O lifecycle dos pods no Kubernetes é o ciclo de vida que um pod passa desde a sua criação até a sua exclusão. O lifecycle dos pods é composto por diferentes
fases, cada uma representando um estado específico do pod. As fases do lifecycle dos pods incluem:

- `Pending`: O pod foi criado, mas ainda não foi atribuído a um nó do cluster para execução. Ele está aguardando recursos disponíveis para ser agendado.
- `Running`: O pod foi atribuído a um nó do cluster e está em execução. Ele pode estar em execução, mas ainda não está pronto para receber tráfego.
- `Succeeded`: O pod foi concluído com sucesso e não está mais em execução. Ele pode ter sido concluído com sucesso ou ter sido concluído devido a um erro, mas
  não está mais em execução.
- `Failed`: O pod foi concluído com falha e não está mais em execução. Ele pode ter sido concluído devido a um erro ou ter sido concluído com sucesso, mas não
  está mais em execução.
- `Unknown`: O estado do pod é desconhecido, geralmente devido a um problema de comunicação com o nó do cluster onde o pod está em execução. O Kubernetes não
  tem informações suficientes para determinar o estado do pod.

O lifecycle dos pods é importante para entender o estado atual de um pod e para monitorar o comportamento dos pods dentro do cluster Kubernetes. Ele permite
que os usuários identifiquem se um pod está em execução, se foi concluído com sucesso ou se ocorreu um erro durante a execução. O lifecycle dos pods é
gerenciado pelo Kubernetes e pode ser monitorado usando o comando `kubectl get pods` para verificar o estado dos pods e tomar as ações necessárias com base no
estado atual dos pods dentro do cluster Kubernetes. Certifique-se de entender o lifecycle dos pods para gerenciar e monitorar os recursos do cluster
Kubernetes de forma eficiente usando o kubectl.
Tambem existe a possibilidade de no yaml do pod configurar os lifecycle hooks, que são ganchos de ciclo de vida que permitem executar comandos ou scripts em
momentos específicos do lifecycle dos pods, como durante a inicialização ou antes da exclusão do pod. Os lifecycle hooks são definidos na seção `lifecycle` do
arquivo de configuração do pod e podem ser usados para realizar tarefas de configuração, limpeza ou outras ações necessárias durante o lifecycle dos pods. Os
lifecycle hooks são úteis para garantir que as ações necessárias sejam executadas em momentos específicos do lifecycle dos pods, permitindo que os usuários
personalizem o comportamento dos pods de acordo com as necessidades da aplicação e do ambiente do cluster Kubernetes usando o kubectl. Certifique-se de
configurar os lifecycle hooks corretamente para garantir que eles sejam executados com sucesso e que o comportamento dos pods seja personalizado de acordo com
as necessidades da aplicação e do ambiente do cluster Kubernetes.
E juntamente tem a possibilidade de configurar o terminationGracePeriodSeconds, que é o tempo de espera em segundos que o Kubernetes aguarda antes de forçar a
exclusão de um pod. Ele é usado para garantir que os pods tenham tempo suficiente para realizar tarefas de limpeza ou outras ações necessárias antes de serem
excluídos do cluster Kubernetes. O terminationGracePeriodSeconds é definido na seção `spec` do arquivo de configuração do pod e pode ser configurado de acordo
com as necessidades da aplicação e do ambiente do cluster Kubernetes. Certifique-se de configurar o terminationGracePeriodSeconds corretamente para garantir que
os pods tenham tempo suficiente para realizar as ações necessárias antes de serem excluídos do cluster Kubernetes, evitando a perda de dados ou interrupção da
aplicação durante o processo de exclusão dos pods usando o kubectl.
Abaixo está um exemplo de configuração de lifecycle hooks e terminationGracePeriodSeconds em um arquivo YAML para um pod do Kubernetes:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: worker-pod
  name: worker-pod
spec:
  terminationGracePeriodSeconds: 60
  containers:
    - image: alpine
      name: alpine
      command: [ "sleep", "infinity" ]
      lifecycle:
        preStop:
          exec:
            command: [ "/bin/sh", "-c", "curl 10.244.2.11" ]
```

Neste exemplo, o pod chamado worker-pod tem um lifecycle hook preStop configurado para executar um comando curl para um endereço IP específico antes de ser
excluído do cluster Kubernetes. O terminationGracePeriodSeconds está configurado para 60 segundos, o que significa que o Kubernetes aguardará até 60 segundos
para que o pod execute o comando preStop e realize as ações necessárias antes de forçar a exclusão do pod. Certifique-se de configurar os lifecycle hooks e o
terminationGracePeriodSeconds de acordo com as necessidades da sua aplicação e do ambiente do cluster Kubernetes para garantir que eles sejam executados com
sucesso e que o comportamento dos pods seja personalizado de acordo com as necessidades da aplicação e do ambiente do cluster Kubernetes usando o kubectl.

--Deployments
No Kubernetes, um deployment é um recurso que gerencia a implantação e a atualização de um conjunto de réplicas de pods. Ele é usado para garantir que um número
específico de réplicas de pods esteja sempre em execução, mesmo em caso de falhas ou indisponibilidade de nós do cluster. O deployment é definido em um arquivo
de configuração YAML que especifica o número desejado de réplicas, a imagem do contêiner a ser usada e outras configurações relevantes para a implantação dos
pods. O deployment é gerenciado pelo control plane do Kubernetes, que monitora o estado dos pods e garante que o número desejado de réplicas esteja sempre em
execução. O deployment é útil para garantir a alta disponibilidade e a escalabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os
usuários criem e gerenciem recursos de forma eficiente usando o kubectl.

Para subir uma aplicação para rodar de verdade em abientes de qa, desenvolvimento ou produção, é recomendado usar um desses tres tipos, sendo o deployment,
statefulset ou um daemonset. Em termos simples o deployment vai ser para aplicações stateless, ou seja, que não precisam de armazenamento persistente, o
statefulset é para aplicações stateful, ou seja, que precisam de armazenamento persistente, e o daemonset é para aplicações que precisam ser executadas em todos
os nós do cluster Kubernetes, como agentes de monitoramento ou coleta de logs. O deployment é o recurso mais comum para implantar aplicativos e serviços dentro
do cluster Kubernetes, e é recomendado para a maioria dos casos de uso, a menos que haja requisitos específicos que exijam o uso de statefulsets ou daemonsets.
Certifique-se de escolher o recurso de implantação adequado para as necessidades da sua aplicação e do ambiente do cluster Kubernetes para garantir que ela seja
implantada e gerenciada de forma eficiente usando o kubectl.

No deployment, é possível configurar a estratégia de atualização para controlar como as atualizações dos pods são realizadas. As estratégias de atualização
disponíveis
são:

- RollingUpdate, que é a estratégia padrão e realiza atualizações de forma gradual, substituindo os pods antigos por novos de forma controlada para garantir
  a disponibilidade da aplicação durante o processo de atualização;
- Recreate, que é uma estratégia mais agressiva que exclui todos os pods antigos antes de criar os novos, o que pode resultar em downtime para a aplicação
  durante o processo de atualização;
- BlueGreen, que é uma estratégia que cria um novo conjunto de pods com a nova versão da aplicação e, em seguida, redireciona o tráfego para os novos pods,
  permitindo uma transição suave entre as versões da aplicação sem
  downtime.

Certifique-se de configurar a estratégia de atualização de acordo com as necessidades da sua aplicação e do ambiente do cluster Kubernetes para
garantir que as atualizações sejam realizadas de forma eficiente e que a disponibilidade da aplicação seja mantida durante o processo de atualização usando o
kubectl.

Abaixo está um exemplo de configuração de deployment em um arquivo YAML para um deployment do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
    environment: development
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: { }
  template:
    metadata:
      labels:
        app: nginx
        environment: development
    spec:
      containers:
        - image: nginx
          name: nginx
          resources: { }
```

Neste exemplo, o deployment chamado nginx é configurado para criar um pod com um contêiner que executa a imagem do nginx. O número de réplicas está definido
como 1, o que significa que apenas um pod será criado para esse deployment. A estratégia de atualização está configurada como padrão (RollingUpdate), o que
significa que as atualizações serão realizadas de forma gradual para garantir a disponibilidade da aplicação durante o processo de atualização. Certifique-se de
configurar os deployments de acordo com as necessidades da sua aplicação e do ambiente do cluster Kubernetes para garantir que eles sejam executados com sucesso
e que os aplicativos e serviços dentro do cluster Kubernetes funcionem corretamente usando o kubectl.

Uma forma de poder alterar a quantidade de réplicas de um deployment é usando o comando
`kubectl scale deployment <nome-do-deployment> --replicas=<número-de-réplicas>`, onde `<nome-do-deployment>` é o nome do deployment que você deseja escalar, e
`<número-de-réplicas>` é o número desejado de réplicas que você deseja para o deployment. Por exemplo, se você quiser escalar um deployment chamado nginx para 3
réplicas, pode usar o comando `kubectl scale deployment nginx --replicas=3`. Isso permitirá que você ajuste a quantidade de réplicas de um deployment de forma
rápida e eficiente usando o kubectl, garantindo que a aplicação tenha a quantidade adequada de réplicas para atender à demanda e garantir a alta disponibilidade
dentro do cluster Kubernetes.

--Labels e selectors
No Kubernetes, labels são pares de chave-valor que são atribuídos a objetos do Kubernetes, como pods, serviços e deployments, para identificar e organizar esses
objetos de forma eficiente. Os labels são usados para agrupar e selecionar objetos com base em critérios específicos, permitindo que os usuários filtrem e
selecionem objetos de forma eficiente dentro do cluster Kubernetes. Os selectors são usados para selecionar objetos com base nos labels atribuídos a eles. Os
selectors podem ser usados em recursos como deployments, services e outros objetos do Kubernetes para selecionar os objetos que correspondem a determinados
critérios de labels. Os selectors podem ser usados para criar relacionamentos entre objetos do Kubernetes, como associar um serviço a um conjunto de pods com
labels específicos. Os labels e selectors são fundamentais para a organização e gerenciamento eficiente dos recursos do Kubernetes, permitindo que os usuários
criem e gerenciem recursos de forma eficiente dentro do cluster Kubernetes usando o kubectl.

--comandos relacionados a deployments
`kubectl create deployment <nome-do-deployment> --image=<imagem-do-container>` -> cria um novo deployment com um contêiner específico, permitindo que os
usuários
implantem aplicativos e serviços dentro do cluster Kubernetes usando o kubectl.
`kubectl create deployment <nome-do-deployment> --image=<imagem-do-container> --replicas=<número-de-réplicas>` -> cria um novo deployment com um contêiner
específico e um número desejado de réplicas, permitindo que os usuários implantem aplicativos e serviços com alta disponibilidade dentro do cluster Kubernetes
usando o kubectl.
`kubectl create deployment <nome-do-deployment> --image=<imagem-do-container> --dry-run -oyaml` -> gera um arquivo YAML de configuração para um deployment com
um
contêiner específico, permitindo que os usuários criem um arquivo de configuração para o deployment e personalizem suas configurações antes de aplicá-lo ao
cluster Kubernetes usando o kubectl.
`kubectl create deployment <nome-do-deployment> --image=<imagem-do-container> --dry-run -oyaml > <arquivo.yaml>` -> gera um arquivo YAML de configuração para um
deployment com um contêiner específico e salva o arquivo em um local especificado, permitindo que os usuários criem um arquivo de configuração para o deployment
e personalizem suas configurações antes de aplicá-lo ao cluster Kubernetes usando o kubectl.
`kubectl get deployments` -> lista os deployments em um cluster Kubernetes, mostrando informações como nome, número de réplicas, status e outros detalhes
relevantes para monitoramento e administração dos recursos do cluster Kubernetes usando o kubectl.
`kubectl describe deployment <nome-do-deployment>` -> exibe detalhes sobre um deployment específico, incluindo informações sobre os pods gerenciados pelo
deployment, eventos relacionados e outros detalhes importantes para a depuração e administração do deployment usando o kubectl.
`kubectl apply -f <arquivo.yaml>` -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de configuração YAML, criando ou atualizando o
recurso
conforme necessário, permitindo que os usuários gerenciem recursos do Kubernetes de forma eficiente usando o kubectl.
`kubectl delete deployment <nome-do-deployment>` -> exclui um deployment específico do cluster Kubernetes, permitindo que os usuários removam deployments que
não
são mais necessários ou que estão causando problemas no cluster usando o kubectl.
`kubectl get deployments -n <nome-do-namespace>` -> lista os deployments em um namespace específico, mostrando informações como nome, número de réplicas, status
e
outros detalhes relevantes para monitoramento e administração dos recursos dentro do namespace usando o kubectl.
`kubectl describe deployment <nome-do-deployment> -n <nome-do-namespace>` -> exibe detalhes sobre um deployment específico em um namespace específico, incluindo
informações sobre os pods gerenciados pelo deployment, eventos relacionados e outros detalhes importantes para a depuração e administração do deployment dentro
do namespace usando o kubectl.
`kubectl delete deployment <nome-do-deployment> -n <nome-do-namespace>` -> exclui um deployment específico de um namespace específico do cluster Kubernetes,
permitindo que os usuários removam deployments de forma mais granular e organizada dentro do cluster usando o kubectl, garantindo que os recursos sejam
gerenciados de forma eficiente dentro dos namespaces do cluster Kubernetes.
`kubectl explain deployment <nome-do-deployment>` -> exibe uma explicação detalhada sobre um deployment específico, incluindo informações sobre os campos de
configuração,
opções disponíveis e exemplos de uso, permitindo que os usuários entendam melhor como configurar e gerenciar deployments dentro do cluster Kubernetes usando o
kubectl. Certifique-se de usar o comando `kubectl explain deployment` para obter informações detalhadas sobre os deployments e garantir que eles sejam
configurados corretamente para atender às necessidades da sua aplicação e do ambiente do cluster Kubernetes usando o kubectl.

--Gerenciamento de rolling updates
No Kubernetes, o gerenciamento de rolling updates é uma estratégia de atualização que permite atualizar os pods de um deployment de forma gradual, garantindo a
disponibilidade da aplicação durante o processo de atualização. O Kubernetes gerencia os rolling updates automaticamente, substituindo os pods antigos por novos
de forma controlada, garantindo que a aplicação continue funcionando durante a atualização. O Kubernetes monitora o estado dos pods durante o processo de
atualização e garante que o número desejado de réplicas esteja sempre em execução, mesmo durante a atualização. O gerenciamento de rolling updates é útil para
garantir a alta disponibilidade e a escalabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários atualizem suas aplicações
de forma eficiente e sem downtime usando o kubectl. Além disso, é possível
configurar a estratégia de atualização para controlar como as atualizações dos pods são realizadas, como RollingUpdate, Recreate ou BlueGreen, para atender às
necessidades específicas da sua aplicação e do ambiente do cluster Kubernetes usando o kubectl.
Para poder otimizar o processo de rolling updates, é possivel configurar os parâmetros de maxUnavailable e maxSurge, que controlam o número máximo de pods que
podem estar indisponíveis durante a atualização e o número máximo de pods que podem ser criados além do número desejado de réplicas durante aatualização,
respectivamente. Esses parâmetros são configurados na seção `strategy` do arquivo de configuração do deployment e podem ser ajustados de acordo com as
necessidades da aplicação e do ambiente do cluster Kubernetes para garantir que o processo de rolling updates seja realizado de forma eficiente e que a
disponibilidade da aplicação seja mantida durante o processo de atualização usando o kubectl.
Abaixo está um exemplo de configuração de maxUnavailable e maxSurge em um arquivo YAML para um deployment do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
    environment: development
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: {
    type: RollingUpdate,
    rollingUpdate: {
      maxUnavailable: 1,
      maxSurge: 1
    }
  }
  template:
    metadata:
      labels:
        app: nginx
        environment: development
    spec:
      containers:
        - image: nginx
          name: nginx
          resources: { }
```

--comandos relacionados a rolling updates
`kubectl rollout status deployment/<nome-do-deployment>` -> exibe o status do rollout de um deployment específico, mostrando informações sobre o progresso da
atualização, o número de pods atualizados e outros detalhes relevantes para monitoramento e administração do processo de atualização usando o kubectl.
`kubectl rollout history deployment/<nome-do-deployment>` -> exibe o histórico de rollouts de um deployment específico, mostrando informações sobre as versões
anteriores do deployment, as mudanças realizadas e outros detalhes relevantes para monitoramento e administração do processo de atualização usando o kubectl.
`kubectl rollout undo deployment/<nome-do-deployment>` -> desfaz a última atualização de um deployment específico, revertendo para a versão anterior do
deployment, permitindo que os usuários revertam rapidamente para uma versão estável em caso de problemas durante o processo de atualização usando o kubectl.
`kubectl rollout undo deployment/<nome-do-deployment> --to-revision=<número-da-revisão>` -> desfaz uma atualização específica de um deployment, revertendo para
uma versão anterior do deployment com base no número da revisão, permitindo que os usuários revertam para uma versão específica em caso de problemas durante o
processo de atualização usando o kubectl.
`kubectl rollout pause deployment/<nome-do-deployment>` -> pausa o processo de atualização de um deployment específico, permitindo que os usuários interrompam
temporariamente o processo de atualização para realizar verificações ou ajustes antes de retomar a atualização usando o kubectl.
`kubectl rollout resume deployment/<nome-do-deployment>` -> retoma o processo de atualização de um deployment específico que foi pausado, permitindo que os
usuários continuem o processo de atualização após realizar verificações ou ajustes necessários usando o kubectl.
`kubectl rollout restart deployment/<nome-do-deployment>` -> reinicia os pods de um deployment específico, forçando a criação de novos pods com a mesma
configuração, permitindo que os usuários reiniciem os pods para aplicar mudanças de configuração ou resolver problemas sem alterar a versão do deployment usando
o kubectl. Certifique-se de usar os comandos de rollout de forma adequada para gerenciar o processo de atualização dos deployments e garantir que a
disponibilidade da aplicação seja mantida durante o processo de atualização usando o kubectl.

--Resources requests e limits
No Kubernetes, os recursos requests e limits são usados para gerenciar os recursos de computação, como CPU e memória, que um contêiner pode solicitar e usar
dentro de um pod. Os recursos requests são a quantidade mínima de recursos que um contêiner precisa para ser agendado e executado, enquanto os recursos limits
são a quantidade máxima de recursos que um contêiner pode usar. Os recursos requests e limits são configurados na seção `resources` do arquivo de configuração
do pod e podem ser ajustados de acordo com as necessidades da aplicação e do ambiente do cluster Kubernetes para garantir que os contêineres tenham os recursos
necessários para funcionar corretamente, sem exceder os limites de recursos disponíveis no cluster Kubernetes. O uso adequado de recursos requests e limits é
fundamental para garantir a eficiência e a estabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem os
recursos de forma eficiente usando o kubectl. O request é a garantia do que é necessario para o pod iniciar, e o limit é o limite máximo que o pod pode usar, ou
seja, se o pod tentar usar mais do que o limite configurado, ele pode ser restringido ou até mesmo ser encerrado pelo Kubernetes para evitar o consumo excessivo
de recursos e garantir a estabilidade do cluster Kubernetes.
Abaixo está um exemplo de configuração de recursos requests e limits em um arquivo YAML para um pod do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
    environment: development
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: {
    type: RollingUpdate,
    rollingUpdate: {
      maxUnavailable: 1,
      maxSurge: 1
    }
  }
  template:
    metadata:
      labels:
        app: nginx
        environment: development
    spec:
      containers:
        - image: nginx
          name: nginx
          resources: {
            requests: {
              cpu: "250m",
              memory: "512Mi"
            },
            limits: {
              cpu: "500m",
              memory: "1024Mi"
            }
          }
```

Neste exemplo, o contêiner nginx tem recursos requests configurados para 250 millicores de CPU e 512 MiB de memória, o que significa que ele precisa de pelo
menos essa quantidade de recursos para ser agendado e executado. Os recursos limits estão configurados para 500 millicores de CPU e 1024 MiB de memória, o que
significa que o contêiner não pode usar mais do que essa quantidade de recursos.

--Goldilocks
Goldilocks é uma ferramenta de código aberto para otimizar os recursos de computação em clusters Kubernetes. Ele analisa o uso de recursos dos pods e fornece
recomendações para ajustar os recursos requests e limits de forma eficiente, garantindo que os contêineres tenham os recursos necessários para funcionar
corretamente, sem exceder os limites de recursos disponíveis no cluster Kubernetes. O Goldilocks é útil para garantir a eficiência e a estabilidade dos
aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários otimizem os recursos de forma eficiente usando o kubectl. Ele pode ser instalado
e configurado no cluster Kubernetes para monitorar o uso de recursos dos pods e fornecer recomendações de otimização, ajudando os usuários a gerenciar os
recursos de forma eficiente e garantir a estabilidade do cluster Kubernetes. Um ponto é que o goldilock não monitora pods diretamente, ele monitora deployments,
statefulsets e daemonsets, ou seja, ele monitora os recursos de computação dos pods gerenciados por esses recursos, fornecendo recomendações de otimização com
base no uso de recursos desses pods, permitindo que os usuários otimizem os recursos de forma eficiente dentro do cluster Kubernetes usando o kubectl.

--Instalação do Goldilocks
Para instalar o Goldilocks no cluster Kubernetes, siga os passos abaixo:

1. Adicione o repositório do Goldilocks ao Helm:
   ```bash
   helm repo add fairwinds-stable https://charts.fairwinds.com/stable
   helm repo update
   ```
2. Instale o Goldilocks usando o Helm:
   ```bash
   helm install goldilocks fairwinds-stable/goldilocks --namespace goldilocks --create-namespace -f values.yaml
   ```
3. O arquivo `values.yaml` você pode pegar em https://artifacthub.io/packages/helm/fairwinds-stable/goldilocks, onde você vai pegar os valores default e vai
   ativar o `vpa` e o `metricsServer` para que o Goldilocks possa coletar os dados de uso de recursos dos pods e fornecer recomendações de otimização.
4. Verifique se o Goldilocks foi instalado corretamente:
   ```bash
   kubectl get pods -n goldilocks
   ```
5. Configure o Goldilocks para monitorar os namespaces desejados, editando o arquivo de configuração do Goldilocks e adicionando os namespaces que você deseja
   monitorar.
   ```bash
   kubectl label ns <namespace-para-monitorar> goldilocks.fairwinds.com/enabled=true
   ```
6. Aguarde alguns minutos para que o Goldilocks colete dados de uso de recursos dos pods e forneça recomendações de otimização.
7. Verifique as recomendações do Goldilocks usando o comando:
   ```bash
   kubectl get vpa -n <namespace>
   ```
8. Aplique as recomendações do Goldilocks para otimizar os recursos dos pods usando o comando:
   ```bash
   kubectl apply -f <arquivo-de-recomendações.yaml>
   ```
9. Para poder visualizar os dados em um dashboard, é possível instalar o Goldilocks Dashboard usando o comando:
   ```bash
   kubectl -n goldilocks port-forward svc/goldilocks-dashboard 8080:80
   ```
10. Depois basta acessar o dashboard em `http://localhost:8080` para visualizar os dados de uso de recursos dos pods e as recomendações de otimização fornecidas
    pelo Goldilocks. No dashboard, você pode visualizar os dados de uso de recursos dos pods, as recomendações de otimização e outras informações relevantes
    para gerenciar os recursos de forma eficiente dentro do cluster Kubernetes usando o kubectl. De preferenia para o Burstable QoS, para que o Goldilocks possa
    fornecer recomendações de otimização mais precisas e eficientes para os recursos de computação dos pods dentro do cluster Kubernetes usando o kubectl.

Certifique-se de seguir as instruções de instalação e configuração do Goldilocks corretamente para garantir que ele funcione corretamente e forneça
recomendações de otimização eficientes para os recursos de computação dentro do cluster Kubernetes usando o kubectl. O Goldilocks é uma ferramenta poderosa para
otimizar os recursos de computação e garantir a eficiência e a estabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários
gerenciem os recursos de forma eficiente usando o kubectl.

--commandos relacionados ao Goldilocks
`kubectl get vpa -n <namespace>` -> exibe as recomendações de otimização de recursos fornecidas pelo Goldilocks para os pods em um namespace específico,
mostrando informações sobre os recursos requests e limits recomendados para cada pod, permitindo que os usuários otimizem os recursos de forma eficiente dentro
do cluster Kubernetes usando o kubectl.
`kubectl apply -f <arquivo-de-recomendações.yaml>` -> aplica as recomendações de otimização fornecidas pelo Goldilocks para os pods, ajustando os recursos
requests e limits de acordo com as recomendações, permitindo que os usuários otimizem os recursos de forma eficiente dentro do cluster Kubernetes usando o
kubectl.
`kubectl describe vpa -n <namespace> <nome-do-pod>` -> exibe detalhes sobre as recomendações de otimização fornecidas pelo Goldilocks para um pod específico,
mostrando informações sobre os recursos requests e limits recomendados, as mudanças sugeridas e outros detalhes relevantes para otimizar os recursos de forma
eficiente dentro do cluster Kubernetes usando o kubectl.

--Probes (health checks)
As probes, ou health checks, são mecanismos de monitoramento usados no Kubernetes para verificar a saúde e o status dos contêineres dentro de um pod. Elas são
usadas para garantir que os contêineres estejam funcionando corretamente e para tomar ações corretivas, como reiniciar um contêiner que esteja com problemas.
Existem três tipos principais de probes no Kubernetes: liveness probe, readiness probe e startup probe. A liveness probe verifica se um contêiner está vivo e
funcionando, a readiness probe verifica se um contêiner está pronto para receber tráfego, e a startup probe verifica se um contêiner está iniciando
corretamente. As probes são configuradas na seção `containers` do arquivo de configuração do pod e podem ser ajustadas de acordo com as necessidades da
aplicação e do ambiente do cluster Kubernetes para garantir que os contêineres sejam monitorados de forma eficiente e que as ações corretivas sejam tomadas
quando necessário usando o kubectl. O uso adequado de probes é fundamental para garantir a estabilidade e a disponibilidade dos aplicativos e serviços dentro do
cluster Kubernetes, permitindo que os usuários monitorem a saúde dos contêineres e tomem ações corretivas de forma eficiente usando o kubectl.
Abaixo está um exemplo de configuração de probes em um arquivo YAML para um pod do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: { }
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - image: nginx
          name: nginx
          resources: { }
          #readinessProbe:
          #  httpGet:
          #    path: "/"
          #    port: 80
          livenessProbe:
            httpGet:
              path: /
              port: 80
```

--Variáveis de ambiente
As variáveis de ambiente são usadas no Kubernetes para fornecer informações de configuração e dados para os contêineres dentro de um pod. Elas são usadas para
configurar o comportamento dos contêineres e para fornecer dados sensíveis, como senhas ou chaves de API, de forma segura. As variáveis de ambiente são
configuradas na seção `containers` do arquivo de configuração do pod e podem ser ajustadas de acordo com as necessidades da aplicação e do ambiente do cluster
Kubernetes para garantir que os contêineres tenham as informações necessárias para funcionar corretamente usando o kubectl. As variáveis de ambiente podem ser
definidas diretamente no arquivo de configuração do pod ou podem ser referenciadas a partir de ConfigMaps ou Secrets, permitindo que os usuários gerenciem as
informações de configuração e os dados sensíveis de forma eficiente dentro do cluster Kubernetes usando o kubectl.
Abaixo está um exemplo de configuração de variáveis de ambiente em um arquivo YAML para um pod do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: { }
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - image: nginx
          name: nginx
          resources: { }
          env:
            - name: "ENVIRONMENT"
              value: "development"
            - name: "LOG_LEVEL"
              value: "debug"
```

--Daemonsets
No Kubernetes, um DaemonSet é um recurso que garante que uma cópia de um pod seja executada em cada nó do cluster Kubernetes. Ele é usado para implantar
aplicativos ou serviços que precisam ser executados em todos os nós do cluster, como agentes de monitoramento, coleta de logs ou outros serviços de
infraestrutura. O DaemonSet é definido em um arquivo de configuração YAML que especifica a imagem do contêiner a ser usada e outras configurações relevantes
para a implantação dos pods. O DaemonSet é gerenciado pelo control plane do Kubernetes, que monitora o estado dos pods e garante que uma cópia do pod esteja
sempre em execução em cada nó do cluster Kubernetes. O DaemonSet é útil para garantir a consistência e a disponibilidade dos aplicativos ou serviços que
precisam ser executados em todos os nós do cluster Kubernetes, permitindo que os usuários criem e gerenciem recursos de forma eficiente usando o kubectl.

Abaixo está um exemplo de configuração de DaemonSet em um arquivo YAML para um DaemonSet do Kubernetes:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - image: nginx
          name: nginx
          resources: { }
      nodeSelector:
        kubernetes.io/hostname: comunidade-devops-worker
```

--Comandos relacionados a DaemonSets
`kubectl create daemonset <nome-do-daemonset> --image=<imagem-do-container>` -> cria um novo DaemonSet com um contêiner específico, permitindo que os usuários
implantem aplicativos ou serviços que precisam ser executados em todos os nós do cluster Kubernetes usando o kubectl.
`kubectl create daemonset <nome-do-daemonset> --image=<imagem-do-container> --dry-run -oyaml` -> gera um arquivo YAML de configuração para um DaemonSet com um
contêiner específico, permitindo que os usuários criem um arquivo de configuração para o DaemonSet e personalizem suas configurações antes de aplicá-lo ao
cluster Kubernetes usando o kubectl.
`kubectl create daemonset <nome-do-daemonset> --image=<imagem-do-container> --dry-run -oyaml > <arquivo.yaml>` -> gera um arquivo YAML de configuração para um
DaemonSet com um contêiner específico e salva o arquivo em um local especificado, permitindo que os usuários criem um arquivo de configuração para o DaemonSet e
personalizem suas configurações antes de aplicá-lo ao cluster Kubernetes usando o kubectl.
`kubectl get daemonsets` -> lista os DaemonSets em um cluster Kubernetes, mostrando informações como nome, número de pods, status e outros detalhes relevantes
para monitoramento e administração dos recursos do cluster Kubernetes usando o kubectl.
`kubectl describe daemonset <nome-do-daemonset>` -> exibe detalhes sobre um DaemonSet específico, incluindo informações sobre os pods gerenciados pelo
DaemonSet, eventos relacionados e outros detalhes importantes para a depuração e administração do DaemonSet usando o kubectl.
`kubectl apply -f <arquivo.yaml>` -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de configuração YAML, criando ou atualizando o
recurso conforme necessário, permitindo que os usuários gerenciem recursos do Kubernetes de forma eficiente usando o kubectl.
`kubectl delete daemonset <nome-do-daemonset>` -> exclui um DaemonSet específico do cluster Kubernetes, permitindo que os usuários removam DaemonSets que não
são mais necessários ou que estão causando problemas no cluster usando o kubectl.
`kubectl get daemonsets -n <nome-do-namespace>` -> lista os DaemonSets em um namespace específico, mostrando informações como nome, número de pods, status e
outros detalhes relevantes para monitoramento e administração dos recursos dentro do namespace usando o kubectl.
`kubectl describe daemonset <nome-do-daemonset> -n <nome-do-namespace>` -> exibe detalhes sobre um DaemonSet específico em um namespace específico, incluindo
informações sobre os pods gerenciados pelo DaemonSet, eventos relacionados e outros detalhes importantes para a depuração e administração do DaemonSet dentro do
namespace usando o kubectl.
`kubectl delete daemonset <nome-do-daemonset> -n <nome-do-namespace>` -> exclui um DaemonSet específico de um namespace específico do cluster Kubernetes,
permitindo que os usuários removam DaemonSets de forma mais granular e organizada dentro do cluster usando o kubectl, garantindo que os recursos sejam
gerenciados de forma eficiente dentro dos namespaces do cluster Kubernetes.
`kubectl explain daemonset <nome-do-daemonset>` -> exibe uma explicação detalhada sobre um DaemonSet específico, incluindo informações sobre os campos de
configuração, opções disponíveis e exemplos de uso, permitindo que os usuários entendam melhor como configurar e gerenciar DaemonSets dentro do cluster
Kubernetes usando o kubectl.

--StatefulSets
No Kubernetes, um StatefulSet é um recurso que gerencia a implantação e a escalabilidade de aplicativos stateful, ou seja, aplicativos que precisam de
armazenamento persistente e identificação única para cada instância. O StatefulSet é usado para implantar aplicativos como bancos de dados, sistemas de
mensagens ou outros aplicativos que exigem armazenamento persistente e identificação única para cada instância. O StatefulSet é definido em um arquivo de
configuração YAML que especifica a imagem do contêiner a ser usada,o número desejado de réplicas, as políticas de atualização e outras configurações relevantes
para a implantação dos pods. O StatefulSet é gerenciado pelo control plane do Kubernetes, que monitora o estado dos pods e garante que o número desejado de
réplicas esteja sempre em execução, mesmo durante o processo de atualização. O StatefulSet é útil para garantir a alta disponibilidade e a escalabilidade dos
aplicativos stateful dentro do cluster Kubernetes, permitindo que os usuários criem e gerenciem recursos de forma eficiente usando o kubectl.
Existe o stateful e o stateless, o stateful é para aplicações que precisam de armazenamento persistente, ou seja, que precisam manter o estado entre as
reinicializações dos pods, como bancos de dados, sistemas de mensagens ou outros aplicativos que exigem armazenamento persistente e identificação única para
cada instância. Já o stateless é para aplicações que não precisam de armazenamento persistente, ou seja, que não precisam manter o estado entre as
reinicializações dos pods, como servidores web, serviços de API ou outros aplicativos que não exigem armazenamento persistente e identificação única para cada
instância. O StatefulSet é recomendado para aplicativos stateful, enquanto o Deployment é recomendado para aplicativos stateless, permitindo que os usuários
escolham o recurso de implantação adequado para as necessidades da sua aplicação e do ambiente do cluster Kubernetes usando o kubectl. O StatefulSet é uma opção
poderosa para gerenciar aplicativos stateful dentro do cluster Kubernetes, garantindo a alta disponibilidade e a escalabilidade desses aplicativos, permitindo
que os usuários criem e gerenciem recursos de forma eficiente usando o kubectl. Uma das vantagens do StatefulSet é que ele garante a ordem de criação e exclusão
dos pods, ou seja, os pods são criados e excluídos em uma ordem específica, garantindo que os aplicativos stateful sejam implantados e escalados de forma
eficiente dentro do cluster Kubernetes usando okubectl. O StatefulSet também suporta a atualização de pods de forma controlada, garantindo que aplicação
stateful seja atualizada de forma eficiente e sem downtime, permitindo que os usuários gerenciem os aplicativos stateful de forma eficiente dentro do cluster
Kubernetes usando o kubectl. O StatefulSet é uma opção recomendada para aplicativos stateful que exigem armazenamento persistente e identificação única para
cada instância, garantindo a alta disponibilidade e a escalabilidade desses aplicativos dentro do cluster Kubernetes usando o kubectl.

Para poder realizar a persistencia de dados em um StatefulSet, é necessário configurar um PersistentVolume (PV) e um PersistentVolumeClaim (PVC) para cada pod
do StatefulSet. O PV é um recurso do Kubernetes que representa um volume de armazenamento físico, enquanto o PVC é um recurso que solicita um volume de
armazenamento específico para ser usado por um pod. O StatefulSet pode ser configurado para usar PVCs para cada pod, garantindo que cada instância do aplicativo
stateful tenha seu próprio armazenamento persistente. O Kubernetes gerencia a criação e a associação dos PVs e PVCs para cada pod do StatefulSet, garantindo que
os dados sejam persistidos de forma eficiente e segura dentro do cluster Kubernetes usando o kubectl.

Com isso para poder usar em um ambiente on-premises, vamos utilizar o local-path-provisioner, que é um provisionador de armazenamento local para Kubernetes. Ele
permite que os usuários criem volumes persistentes usando o armazenamento local do nó onde o pod está sendo executado. O local-path-provisioner é útil para
ambientes on-premises onde o armazenamento em nuvem não está disponível ou não é desejado, permitindo que os usuários criem volumes persistentes de forma
eficiente usando o armazenamento local do cluster Kubernetes. Para instalar o local-path-provisioner no cluster Kubernetes, siga os passos abaixo:

1. Rode o comando para instalar o local-path-provisioner usando o kubectl:

```bash
   kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.35/deploy/local-path-storage.yaml
```

2. Verifique se o local-path-provisioner foi instalado corretamente:

```bash
   kubectl get pods -n local-path-storage
```

3. Verifique se o local-path-provisioner foi configurado como o provisionador de armazenamento padrão para o cluster Kubernetes:

```bash
   kubectl get storageclass -A
```

4. Caso não esteja configurado como o provisionador de armazenamento padrão, configure o local-path-provisioner como o provisionador de armazenamento padrão
   para o cluster
   Kubernetes, editando o arquivo de configuração do cluster e definindo o local-path-provisioner como o provisionador de armazenamento padrão.

```bash
   kubectl edit storageclass local-path
```

5. No editor de texto que será aberto, adicione a seguinte linha na seção `annotations` do arquivo de configuração do storage class local-path:

```yaml
    storageclass.kubernetes.io/is-default-class: "true"
```

6. Salve e feche o arquivo de configuração do storage class local-path para aplicar as alterações.

Abaixo está um exemplo de configuração de StatefulSet em um arquivo YAML para um StatefulSet do Kubernetes:

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - image: nginx
          name: nginx
          volumeMounts:
            - mountPath: "/usr/share/nginx/html"
              name: nginx-html
  volumeClaimTemplates:
    - metadata:
        name: nginx-html
      spec:
        accessModes: [ "ReadWriteOnce" ]
        resources:
          requests:
            storage: 1G
```

--Comandos relacionados a StatefulSets
`kubectl create statefulset <nome-do-statefulset> --image=<imagem-do-container>` -> cria um novo StatefulSet com um contêiner específico, permitindo que os
usuários implantem aplicativos stateful dentro do cluster Kubernetes usando o kubectl.
`kubectl create statefulset <nome-do-statefulset> --image=<imagem-do-container> --dry-run -oyaml` -> gera um arquivo YAML de configuração para um StatefulSet
com um contêiner específico, permitindo que os usuários criem um arquivo de configuração para o StatefulSet e personalizem suas configurações antes de aplicá-lo
ao cluster Kubernetes usando o kubectl.
`kubectl create statefulset <nome-do-statefulset> --image=<imagem-do-container> --dry-run -oyaml > <arquivo.yaml>` -> gera um arquivo YAML de configuração para
um StatefulSet com um contêiner específico e salva o arquivo em um local especificado, permitindo que os usuários criem um arquivo de configuração para o
StatefulSet e personalizem suas configurações antes de aplicá-lo ao cluster Kubernetes usando o kubectl.
`kubectl get statefulsets` -> lista os StatefulSets em um cluster Kubernetes, mostrando informações como nome, número de réplicas, status e outros detalhes
relevantes para monitoramento e administração dos recursos do cluster Kubernetes usando o kubectl.
`kubectl describe statefulset <nome-do-statefulset>` -> exibe detalhes sobre um StatefulSet específico, incluindo informações sobre os pods gerenciados pelo
StatefulSet, eventos relacionados e outros detalhes importantes para a depuração e administração do StatefulSet usando o kubectl.
`kubectl apply -f <arquivo.yaml>` -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de configuração YAML, criando ou atualizando o
recurso conforme necessário, permitindo que os usuários gerenciem recursos do Kubernetes de forma eficiente usando o kubectl.
`kubectl delete statefulset <nome-do-statefulset>` -> exclui um StatefulSet específico do cluster Kubernetes, permitindo que os usuários removam StatefulSets
que não são mais necessários ou que estão causando problemas no cluster usando o kubectl.
`kubectl get statefulsets -n <nome-do-namespace>` -> lista os StatefulSets em um namespace específico, mostrando informações como nome, número de réplicas,
status e outros detalhes relevantes para monitoramento e administração dos recursos dentro do namespace usando o kubectl.
`kubectl describe statefulset <nome-do-statefulset> -n <nome-do-namespace>` -> exibe detalhes sobre um StatefulSet específico em um namespace específico,
incluindo informações sobre os pods gerenciados pelo StatefulSet, eventos relacionados e outros detalhes importantes para a depuração e administração do
StatefulSet dentro do namespace usando o kubectl.
`kubectl delete statefulset <nome-do-statefulset> -n <nome-do-namespace>` -> exclui um StatefulSet específico de um namespace específico do cluster Kubernetes,
permitindo que os usuários removam StatefulSets de forma mais granular e organizada dentro do cluster usando o kubectl, garantindo que os recursos sejam
gerenciados de forma eficiente dentro dos namespaces do cluster Kubernetes.
`kubectl explain statefulset <nome-do-statefulset>` -> exibe uma explicação detalhada sobre um StatefulSet específico, incluindo informações sobre os campos de
configuração, opções disponíveis e exemplos de uso, permitindo que os usuários entendam melhor como configurar e gerenciar StatefulSets dentro do cluster
Kubernetes usando o kubectl. Certifique-se de usar o comando `kubectl explain statefulset` para obter informações detalhadas sobre os StatefulSets e garantir
que eles sejam configurados corretamente para atender às necessidades da sua aplicação e do ambiente do cluster Kubernetes usando o kubectl.
`kubectl get pvc` -> lista os PersistentVolumeClaims (PVCs) em um cluster Kubernetes, mostrando informações como nome, status, capacidade e outros detalhes
relevantes para monitoramento e administração dos recursos de armazenamento dentro do cluster Kubernetes usando o kubectl.
`kubectl describe pvc <nome-do-pvc>` -> exibe detalhes sobre um PersistentVolumeClaim (PVC) específico, incluindo informações sobre o volume associado, eventos
relacionados e outros detalhes importantes para a depuração e administração do PVC usando o kubectl.
`kubectl delete pvc <nome-do-pvc>` -> exclui um PersistentVolumeClaim (PVC) específico do cluster Kubernetes, permitindo que os usuários removam PVCs que não
são mais necessários ou que estão causando problemas no cluster usando o kubectl.
`kubectl get pv` -> lista os PersistentVolumes (PVs) em um cluster Kubernetes, mostrando informações como nome, status, capacidade e outros detalhes relevantes
para monitoramento e administração dos recursos de armazenamento dentro do cluster Kubernetes usando o kubectl.
`kubectl describe pv <nome-do-pv>` -> exibe detalhes sobre um PersistentVolume (PV) específico, incluindo informações sobre o volume, eventos relacionados e
outros detalhes importantes para a depuração e administração do PV usando o kubectl.
`kubectl delete pv <nome-do-pv>` -> exclui um PersistentVolume (PV) específico do cluster Kubernetes, permitindo que os usuários removam PVs que não são mais
necessários ou que estão causando problemas no cluster usando o kubectl. Certifique-se de usar os comandos relacionados a PVCs e PVs de forma adequada para
gerenciar os recursos de armazenamento dentro do cluster Kubernetes e garantir que os aplicativos stateful tenham acesso ao armazenamento persistente necessário
para funcionar corretamente usando o kubectl.
`kubectl get storageclass` -> lista os StorageClasses em um cluster Kubernetes, mostrando informações como nome, provisionador e outros detalhes relevantes para
monitoramento e administração dos recursos de armazenamento dentro do cluster Kubernetes usando o kubectl.
`kubectl describe storageclass <nome-do-storageclass>` -> exibe detalhes sobre um StorageClass específico, incluindo informações sobre o provisionador,
parâmetros de configuração e outros detalhes importantes para a depuração e administração do StorageClass usando o kubectl.
`kubectl delete storageclass <nome-do-storageclass>` -> exclui um StorageClass específico do cluster Kubernetes, permitindo que os usuários removam
StorageClasses que não são mais necessários ou que estão causando problemas no cluster usando o kubectl. Certifique-se de usar os comandos relacionados a
StorageClasses de forma adequada para gerenciar os recursos de armazenamento dentro do cluster Kubernetes e garantir que os aplicativos stateful tenham acesso
ao armazenamento persistente necessário para funcionar corretamente usando o kubectl.

--Pod disruption budget (PDB)
No Kubernetes, um Pod Disruption Budget (PDB) é um recurso que define as regras para a interrupção de pods em um cluster Kubernetes. Ele é usado para garantir a
disponibilidade e a estabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários definam limites para a quantidade de pods
que podem ser interrompidos durante operações de manutenção, atualizações ou falhas. O PDB é definido em um arquivo de configuração YAML que especifica o número
mínimo de pods que devem estar disponíveis durante uma interrupção, o número máximo de pods que podem ser interrompidos e outras configurações relevantes para a
gestão de interrupções de pods. O PDB é gerenciado pelo control plane do Kubernetes, que monitora o estado dos pods e garante que as regras definidas no PDB
sejam respeitadas durante as operações de manutenção, atualizações ou falhas, garantindo a disponibilidade e a estabilidade dos aplicativos e serviços dentro do
cluster Kubernetes usando o kubectl. O PDB é uma ferramenta importante para garantir a resiliência e a alta disponibilidade dos aplicativos e serviços dentro do
cluster Kubernetes, permitindo que os usuários gerenciem as interrupções de pods de forma eficiente usando o kubectl. O PDB é especialmente útil em ambientes de
produção, onde a disponibilidade dos aplicativos e serviços é crítica, permitindo que os usuários definam regras para garantir que as interrupções de pods sejam
gerenciadas de forma eficiente e que a disponibilidade dos aplicativos e serviços seja mantida durante as operações de manutenção, atualizações ou falhas usando
o kubectl. Segue o link da documentação oficial do Kubernetes sobre Pod Disruption Budget (PDB) para mais
informações: https://kubernetes.io/docs/tasks/run-application/configure-pdb/#think-about-how-your-application-reacts-to-disruptions.
Abaixo está um exemplo de configuração de Pod Disruption Budget (PDB) em um arquivo YAML para um PDB do Kubernetes:

```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: nginx-pdb
spec:
  maxUnavailable: 0
  selector:
    matchLabels:
      app: nginx
```