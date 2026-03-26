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
3. Dentro do contêiner do nó de control plane, você pode encontrar o arquivo admin.config no diretório `/etc/kubernetes/` ou na pasta onde vc rodou o comando
   `create cluster` que vai estar com o nome `config`. Acesse o conteudo do arquivo
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

Antes de instalar o Goldilocks, certifique-se de ter instalado o metrics-server no cluster Kubernetes, pois o Goldilocks depende do metrics-server para coletar
dados de uso de recursos dos pods e fornecer recomendações de otimização. Use o comando `kubectl top pods` para verificar se o metrics-server está funcionando
corretamente e coletando dados de uso de recursos dos pods antes de instalar o Goldilocks. Se o comando `kubectl top pods` não retornar dados de uso de recursos
dos pods, certifique-se de que o metrics-server esteja instalado e configurado corretamente no cluster Kubernetes antes de prosseguir com a instalação do
Goldilocks. Para a instalação do metrics-server, você pode seguir as instruções abaixo:

1. Use o comando `kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml` para instalar o metrics-server no
   cluster Kubernetes.
2. Verifique se o metrics-server foi instalado corretamente usando o comando `kubectl get pods -n kube-system | grep metrics-server` para verificar se os pods
   do metrics-server estão em execução.
3. Aguarde alguns minutos para que o metrics-server colete dados de uso de recursos dos pods e forneça as métricas necessárias para o Goldilocks funcionar
   corretamente.
4. Caso o metrics-server não esteja funcionando corretamente localmente, algo que é comum devido ao TLS, edite o deployment do metrics-server, para abrir o
   arquivo use `kubectl edit deployment metrics-server -n kube-system` e adicione os seguintes argumentos
   para desabilitar a verificação de TLS:
   ```yaml
   template:
    metadata:
      annotations:
        kubectl.kubernetes.io/restartedAt: "2026-03-25T15:33:44-03:00"
      labels:
        k8s-app: metrics-server
    spec:
      containers:
      - args:
        - --kubelet-insecure-tls # Adicione este argumento para desabilitar a verificação de TLS
        - --cert-dir=/tmp
        - --secure-port=10250
        - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
        - --kubelet-use-node-status-port
        - --metric-resolution=15s
   ```
5. Salve o arquivo e execute o comando `kubectl rollout restart deployment metrics-server -n kube-system` para reiniciar o deployment do metrics-server e
   aplicar as alterações
   feitas no arquivo de configuração.
6. Verifique novamente se o metrics-server está funcionando corretamente usando o comando `kubectl top pods` para verificar se os dados de uso de recursos dos
   pods estão sendo coletados corretamente pelo metrics-server, garantindo que o Goldilocks possa coletar os dados necessários para fornecer recomendações de
   otimização eficientes para os recursos de computação dos pods dentro do cluster Kubernetes usando o kubectl.

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

--Comandos relacionados a Pod Disruption Budget (PDB)
`kubectl create pdb <nome-do-pdb> --selector=<seletor-de-labels> --max-unavailable=<número-máximo-de-pods-indisponíveis>` -> cria um novo Pod Disruption
Budget (PDB) com um seletor de labels específico e um número máximo de pods indisponíveis, permitindo que os usuários definam regras para a interrupção de pods
dentro do cluster Kubernetes usando o kubectl.
`kubectl create pdb <nome-do-pdb> --selector=<seletor-de-labels> --max-unavailable=<número-máximo-de-pods-indisponíveis> --dry-run -oyaml` -> gera um arquivo
YAML de configuração para um Pod Disruption Budget (PDB) com um seletor de labels específico e um número máximo de pods indisponíveis, permitindo que os
usuários criem um arquivo de configuração para o PDB e personalizem suas configurações antes de aplicá-lo ao cluster Kubernetes usando o kubectl.
`kubectl create pdb <nome-do-pdb> --selector=<seletor-de-labels> --max-unavailable=<número-máximo-de-pods-indisponíveis> --dry-run -oyaml > <arquivo.yaml>` ->
gera um arquivo YAML de configuração para um Pod Disruption Budget (PDB) com um seletor de labels específico e um número máximo de pods indisponíveis, e salva o
arquivo em um local especificado, permitindo que os usuários criem um arquivo de configuração para o PDB e personalizem suas configurações antes de aplicá-lo ao
cluster Kubernetes usando o kubectl.
`kubectl get pdb` -> lista os Pod Disruption Budgets (PDBs) em um cluster Kubernetes, mostrando informações como nome, número de pods afetados, status e outros
detalhes relevantes para monitoramento e administração dos recursos do cluster Kubernetes usando o kubectl.
`kubectl describe pdb <nome-do-pdb>` -> exibe detalhes sobre um Pod Disruption Budget (PDB) específico, incluindo informações sobre os pods afetados, eventos
relacionados e outros detalhes importantes para a depuração e administração do PDB usando o kubectl.
`kubectl delete pdb <nome-do-pdb>` -> exclui um Pod Disruption Budget (PDB) específico do cluster Kubernetes, permitindo que os usuários removam PDBs que não
são mais necessários ou que estão causando problemas no cluster usando o kubectl.
`kubectl get pdb -n <nome-do-namespace>` -> lista os Pod Disruption Budgets (PDBs) em um namespace específico, mostrando informações como nome, número de pods
afetados, status e outros detalhes relevantes para monitoramento e administração dos recursos dentro do namespace usando o kubectl.
`kubectl describe pdb <nome-do-pdb> -n <nome-do-namespace>` -> exibe detalhes sobre um Pod Disruption Budget (PDB) específico em um namespace específico,
incluindo informações sobre os pods afetados, eventos relacionados e outros detalhes importantes para a depuração e administração do PDB dentrodo namespace
usando o kubectl.
`kubectl delete pdb <nome-do-pdb> -n <nome-do-namespace>` -> exclui um Pod Disruption Budget (PDB) específico de um namespace específico do cluster Kubernetes,
permitindo que os usuários removam PDBs de forma mais granular e organizada dentro do cluster usando o kubectl, garantindo que os recursos sejam gerenciados de
forma eficiente dentro dos namespaces do cluster Kubernetes.
`kubectl explain pdb <nome-do-pdb>` -> exibe uma explicação detalhada sobre um Pod Disruption Budget (PDB) específico, incluindo informações sobre os campos de
configuração, opções disponíveis e exemplos de uso, permitindo que os usuários entendam melhor como configurar e gerenciar Pod Disruption Budgets dentro do
cluster Kubernetes usando o kubectl. Certifique-se de usar o comando `kubectl explain pdb` para obter informações detalhadas sobre os Pod Disruption Budgets e
garantir que eles sejam configurados corretamente para atender às necessidades da sua aplicação e do ambiente do cluster Kubernetes usando o kubectl. O uso
adequado de Pod Disruption Budgets é fundamental para garantir a resiliência e a alta disponibilidade dos aplicativos e serviços dentro do cluster Kubernetes,
permitindo que os usuários gerenciem as interrupções de pods de forma eficiente usando o kubectl.

--Jobs e CronJobs
No Kubernetes, um Job é um recurso que gerencia a execução de tarefas em um cluster Kubernetes. Ele é usado para executar tarefas de forma assíncrona, como
processamento de dados, execução de scripts ou outras tarefas que precisam ser executadas uma única vez ou em um intervalo específico. O Job é definido em um
arquivo de configuração YAML que especifica a imagem do contêiner a ser usada, o comando a ser executado e outras configurações relevantes para a execução da
tarefa. O Job é gerenciado pelo control plane do Kubernetes, que monitora o estado dos pods e garante que a tarefa seja executada de forma eficiente e
confiável, mesmo em caso de falhas ou reinicializações dos pods, garantindo a execução bem-sucedida das tarefas dentro do cluster Kubernetes usando o kubectl. O
Job é uma ferramenta importante para executar tarefas assíncronas dentro do cluster Kubernetes, permitindo que os usuários gerenciem a execução de tarefas de
forma eficiente usando o kubectl. O Job é recomendado para tarefas que precisam ser executadas uma única vez ou em um intervalo específico, enquanto o CronJob é
recomendado para tarefas que precisam ser executadas em um horário específico ou em um intervalo regular, permitindo que os usuários escolham o recurso de
execução de tarefas adequado para as necessidades da sua aplicação e do ambiente do cluster Kubernetes usando o kubectl. O Job é uma opção poderosa para
gerenciar a execução de tarefas dentro do cluster Kubernetes, garantindo a execução bem-sucedida das tarefas mesmo em caso de falhas ou reinicializações dos
pods, permitindo que os usuários gerenciem a execução de tarefas de forma eficiente usando o kubectl. O Job é especialmente útil para tarefas que exigem
processamento de dados, execução de scripts ou outras tarefas que precisam ser executadas de forma assíncrona dentro do cluster Kubernetes, permitindo que os
usuários gerenciem a execução de tarefas de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre Jobs e CronJobs para mais
informações: https://kubernetes.io/docs/concepts/workloads/controllers/job/. Um ponto importante é que um job é imutável, ou seja, uma vez criado, ele não pode
ser modificado. Se for necessário alterar a configuração de um job, é necessário excluí-lo e criá-lo novamente com as novas configurações. Isso garante a
integridade e a consistência dos jobs dentro do cluster Kubernetes, permitindo que os usuários gerenciem a execução de tarefas de forma eficiente usando o
kubectl. Então o ideal é usar a proprieade `ttlSecondsAfterFinished` para definir um tempo de vida para o job após a conclusão, garantindo que os recursos sejam
liberados de forma eficiente dentro do cluster Kubernetes usando okubectl.

Abaixo está um exemplo de configuração de Job em um arquivo YAML para um Job do Kubernetes:

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: echo-command
spec:
  template:
    spec:
      containers:
        - name: sleep
          image: alpine
          command: [ "echo", "Comunidade devops é foda" ]
      restartPolicy: OnFailure
  ttlSecondsAfterFinished: 0
  backoffLimit: 4
```

Exemplo de configuração de CronJob em um arquivo YAML para um CronJob do Kubernetes:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: echo-command
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: sleep
              image: alpine
              command: [ "echo", "Comunidade devops é foda" ]
          restartPolicy: OnFailure
      ttlSecondsAfterFinished: 0
      backoffLimit: 4
```

--Services
No Kubernetes, um Service é um recurso que define uma abstração de rede para acessar os pods dentro de um cluster Kubernetes. Ele é usado para expor os pods
para outros serviços ou para o mundo externo, permitindo que os usuários acessem os aplicativos e serviços dentro do cluster Kubernetes de forma eficiente e
confiável. O Service é definido em um arquivo de configuração YAML que especifica o tipo de serviço, as portas a serem expostas e outras configurações
relevantes para a exposição dos pods. O Service é gerenciado pelo control plane do Kubernetes, que monitora o estado dos pods e garante que o tráfego seja
roteado de forma eficiente para os pods, mesmo em caso de falhas ou reinicializações dos pods, garantindo a disponibilidade e a confiabilidade dos aplicativos e
serviços dentro do cluster Kubernetes usando o kubectl. O Service é uma ferramenta importante para expor os aplicativos e serviços dentro do cluster Kubernetes,
permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. O Service é recomendado para expor os aplicativos e serviços dentro do
cluster Kubernetes, enquanto o Ingress é recomendado para expor os aplicativos e serviços para o mundo externo, permitindo que os usuários escolham o recurso de
exposição adequado para as necessidades da sua aplicação e do ambiente do cluster Kubernetes usando o kubectl. O Service é uma opção poderosa para expor os
aplicativos e serviços dentro do clusterKubernetes, garantindo a disponibilidade e a confiabilidade dos recursos mesmo em caso de falhas ou reinicializações dos
pods, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Os pontos importantes sobre os Services são: o tipo de serviço pode
ser ClusterIP, NodePort, LoadBalancer ou ExternalName, dependendo das necessidades de exposição dos aplicativos e serviços dentro do cluster Kubernetes;

- ClusterIP é o tipo de serviço padrão, que expõe os pods dentro do cluster Kubernetes usando um endereço IP interno;
- NodePort expõe os pods em uma porta específica em cada nó do cluster Kubernetes, permitindo o acesso externo aos pods (pouco usado em ambientes produção);
- LoadBalancer cria um balanceador de carga externo para expor os pods, permitindo o acesso externo aos pods de forma eficiente e confiável, porem é muito
  custoso, ideal para apps TCP ou UDP (mais usado em ambientes de nuvem);
- ExternalName mapeia um nome de serviço para um nome DNS externo, permitindo que os usuários acessem os recursos usando um nome de domínio personalizado. O
  Service também suporta a definição de seletores de labels para direcionar o tráfego para os pods corretos, garantindo que o tráfego seja roteado de forma
  eficiente para os pods dentro do cluster Kubernetes usando o kubectl.

Segue o link da documentação oficial do Kubernetes sobre Services para mais informações: https://kubernetes.io/docs/concepts/services-networking/service/.

Abaixo está um exemplo de configuração de Service em um arquivo YAML para um Service do Kubernetes:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  selector:
    app: nginx
  ports:
    - name: https
      port: 80
      targetPort: 80
  type: ClusterIP
```

--Comandos relacionados a Services
`kubectl create service <tipo-de-serviço> <nome-do-serviço> --tcp=<porta>:<targetPort>` -> cria um novo Service com um tipo de serviço específico e uma
configuração de porta, permitindo que os usuários exponham os aplicativos e serviços dentro do cluster Kubernetes de forma eficiente usando o kubectl.
`kubectl create service <tipo-de-serviço> <nome-do-serviço> --tcp=<porta>:<targetPort> --dry-run -oyaml` -> gera um arquivo YAML de configuração para um Service
com um tipo de serviço específico e uma configuração de porta, permitindo que os usuários criem um arquivo de configuração para o Service e personalizem suas
configurações antes de aplicá-lo ao cluster Kubernetes usando o kubectl.

--Dica usando o kubectl expose
O comando `kubectl expose` é uma maneira rápida e fácil de criar um Service para um recurso existente, como um Deployment, um ReplicaSet ou um Pod. Ele permite
que os usuários exponham os aplicativos e serviços dentro do cluster Kubernetes de forma eficiente usando o kubectl, sem a necessidade de criar um arquivo de
configuração YAML para o Service. O comando `kubectl expose` é recomendado para casos em que os usuários desejam expor rapidamente um recurso existente,
enquanto a criação de um arquivo de configuração YAML é recomendada para casos em que os usuários desejam personalizar as configurações do Service de forma mais
detalhada. O comando `kubectl expose` é uma opção poderosa para expor os aplicativos e serviços dentro do cluster Kubernetes de forma rápida e eficiente usando
o kubectl, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre o
comando `kubectl expose` para mais informações: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#expose.

--Comandos relacionados a kubectl expose
`kubectl expose <tipo-de-recurso> <nome-do-recurso> --port=<porta> --target-port=<targetPort>` -> expõe um recurso existente, como um Deployment, um ReplicaSet
ou um Pod, criando um Service com uma configuração de porta específica, permitindo que os usuários exponham os aplicativos e serviços dentro do cluster
Kubernetes de forma eficiente usando o kubectl.

--Service Discovery(DNS)
No Kubernetes, o Service Discovery é um mecanismo que permite que os aplicativos e serviços dentro do cluster Kubernetes se descubram e se comuniquem entre si
usando nomes de serviço em vez de endereços IP. O Kubernetes fornece um sistema de DNS interno que resolve os nomes de serviço para os endereços IP dos pods
associados ao serviço, permitindo que os aplicativos e serviços se comuniquem de forma eficiente e confiável dentro do cluster Kubernetes usando o kubectl. O
Service Discovery é uma ferramenta importante para garantir a comunicação eficiente entre os aplicativos e serviços dentro do cluster Kubernetes, permitindo que
os usuários acessem os recursos de forma eficiente usando o kubectl. O Service Discovery é recomendado para casos em que os aplicativos e serviços dentro do
cluster Kubernetes precisam se comunicar entre si de forma eficiente e confiável,permitindo que os usuários acessem os recursos de forma eficiente usando o
kubectl. O Service Discovery é uma opção poderosa para garantir a comunicação eficiente entre os aplicativos e serviços dentro do cluster Kubernetes,permitindo
que os usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre Service Discovery para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#discovering-services.
Caso eu esteja em uma service que esteja em um namespace diferente e queira acessar o `nginx` que está em outro namespace, eu posso por exemplo acessa-lo usando
o nome do serviço e o namespace, como `nginx.<namespace>.svc.cluster.local`, ou seja, usando o formato
`<nome-do-serviço>.<nome-do-namespace>.svc.cluster.local`, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl, mesmo quando os
serviços estão em namespaces diferentes dentro do cluster Kubernetes. O uso adequado dos Services é fundamental para garantir a disponibilidade e a
confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl.
E se for um pod e eu tenha o ip dele e queira acessar ele de outro namespace, eu posso acessar ele usando o formato
`<ip-do-pod>.<nome-do-namespace>.pod.cluster.local`, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl, mesmo quando os pods
estão em namespaces diferentes dentro do cluster Kubernetes. O uso adequado dos Services e dos pods é fundamental para garantir a disponibilidade e a
confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl.

--Como uma requisição chega no pod
Quando uma requisição é feita para um serviço no Kubernetes, o processo de roteamento envolve várias etapas para garantir que a requisição seja direcionada
corretamente para os pods que estão atendendo ao serviço. Aqui está um resumo de como uma requisição chega a um pod:

1. O cliente faz uma requisição para o serviço usando o nome do serviço ou o endereço IP do serviço.
2. O Kubernetes usa o sistema de DNS interno para resolver o nome do serviço para o endereço IP do serviço.
3. O Kubernetes verifica as regras de roteamento definidas para o serviço, como as regras de balanceamento de carga e as regras de afinidade, para determinar
   quais pods estão associados ao serviço e como a requisição deve ser roteada.
4. O Kubernetes seleciona um pod que está associado ao serviço com base nas regras de roteamento e encaminha a requisição para o pod selecionado.
5. O pod recebe a requisição e processa a solicitação,gerando uma resposta que é enviada de volta para o cliente através do serviço.
6. O serviço encaminha a resposta do pod de volta para o cliente, garantindo que a comunicação entre o cliente e o pod seja eficiente e confiável dentro do
   cluster Kubernetes usando o kubectl.
   Esse processo de roteamento é gerenciado pelo control plane do Kubernetes, que monitora o estado dos pods e garante que as requisições sejam roteadas de
   forma eficiente para os pods dentro do cluster Kubernetes, mesmo em caso de falhas ou reinicializações dos pods, garantindo a disponibilidade e a
   confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes usando o kubectl. O uso adequado dos Services é fundamental para garantir a
   disponibilidade e a confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários acessem os recursos de forma eficiente
   usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre como as requisições chegam aos pods para mais
   informações: https://kubernetes.io/docs/concepts/services-networking/service/#how-requests-reach-pods.

Caso algum problema de roteamento, verificar porque talvez pode ser um problema relacionado ao selector do service que pode estar mandando para uma label
errada, as labels que esta em pods não estão relacionados aquele serviço ou labels duplicadas.

--Kube-proxy: IPVS mode
O kube-proxy é um componente do Kubernetes que é responsável por gerenciar o roteamento de tráfego para os serviços dentro do cluster Kubernetes. Ele é
executado em cada nó do cluster Kubernetes e é responsável por garantir que as requisições sejam roteadas de forma eficiente para os pods associados aos
serviços. O kube-proxy suporta diferentes modos de operação, incluindo o modo IPVS (IP Virtual Server), que é um modo de balanceamento de carga de alto
desempenho para serviços dentro do cluster Kubernetes. O modo IPVS usa o kernel do Linux para realizar o balanceamento de carga, permitindo que as requisições
sejam roteadas de forma eficiente para os pods associados aos serviços, mesmo em casos de alta carga ou falhas nos pods, garantindo a disponibilidade e a
confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes usando o kubectl. O modo IPVS é recomendado para ambientes de produção que exigem alto
desempenho e escalabilidade para os serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem o roteamento de tráfego de forma eficiente
usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre o kube-proxy e o modo IPVS para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#proxy-mode-ipvs. O uso adequado do kube-proxy e do modo IPVS é fundamental para
garantir a disponibilidade e a confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem o roteamento de
tráfego de forma eficiente usando o kubectl. O kube-proxy é uma parte essencial da infraestrutura de rede do Kubernetes, garantindo que as requisições sejam
roteadas de forma eficiente para os pods associados aos serviços, mesmo em casos de alta carga ou falhas nos pods, garantindo a disponibilidade e a
confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes usando o kubectl. O modo IPVS é uma opção poderosa para ambientes de produção que exigem
alto desempenho e escalabilidade para os serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem oroteamento de tráfego de forma eficiente
usando o kubectl.

Voce pode alterar o modo de operação do kube-proxy para IPVS editando a configuração do cluster Kubernetes e definindo o modo de proxy para IPVS, garantindo que
o kube-proxy use o modo IPVS para gerenciar o roteamento de tráfego para os serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem o
roteamento de tráfego de forma eficiente usando o kubectl. Para alterar o modo de operação do kube-proxy para IPVS, siga os passos abaixo:

1. Edite a configuração do cluster Kubernetes usando o comando `kubectl edit configmap kube-proxy -n kube-system` para abrir o arquivo de configuração do
   kube-proxy em um editor de texto.
2. No arquivo de configuração do kube-proxy, localize a seção `mode` e altere o valor para `ipvs`, garantindo que o kube-proxy use o modo IPVS para gerenciar
   o roteamento de tráfego para os serviços dentro do cluster Kubernetes.
3. Salve e feche o arquivo de configuração do kube-proxy para aplicar as alterações.
4. O kube-proxy será reiniciado automaticamente para aplicar as alterações, garantindo que o modo IPVS seja ativado para gerenciar o roteamento de tráfego para
   os serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem o roteamento de tráfego de forma eficiente usando o kubectl. É importante para
   garantir que as configurações sejam aplicadas, rebutando ou excluindo os pods do kube-proxy para que eles sejam recriados com as novas configurações,
   garantindo que o modo IPVS seja ativado para gerenciar o roteamento de tráfego para os serviços dentro do cluster Kubernetes, permitindo que os usuários
   gerenciem o roteamento de tráfego de forma eficiente usando o kubectl.

--Kube-proxy: Iptables mode
O modo iptables é o modo de proxy padrão para o kube-proxy no Kubernetes. Ele usa o sistema de firewall iptables do Linux para gerenciar o roteamento de tráfego
para os serviços dentro do cluster Kubernetes. O modo iptables é uma opção confiável e amplamente suportada para gerenciar o roteamento de tráfego para os
serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem o roteamento de tráfego de forma eficiente usando o kubectl. O modo iptables é
recomendado para ambientes de desenvolvimento e teste, onde o desempenho e a escalabilidade não são tão críticos, permitindo que os usuários gerenciem o
roteamento de tráfego de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre o kube-proxy e o modo iptables para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#proxy-mode-iptables. O uso adequado do kube-proxy e do modo iptables é fundamental
para garantir a disponibilidade e a confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários gerenciem o roteamento de
tráfego de forma eficiente usando o kubectl. O kube-proxy é uma parte essencial da infraestrutura de rede do Kubernetes, garantindo que as requisições sejam
roteadas de forma eficiente para os pods associados aos serviços, mesmo em casos de alta carga ou falhas nos pods, garantindo a disponibilidade e a
confiabilidade dos aplicativos e serviços dentro do cluster Kubernetes usando o kubectl.
Uma forma de salvar as configurações atuais do iptables é usando o comando `iptables-save > <arquivo-iptables>.txt`, que salva as regras atuais do iptables em
um arquivo de texto, permitindo que os usuários tenham um backup das configurações atuais do iptables antes de fazer alterações, garantindo que as configurações
possam ser restauradas se necessário, permitindo que os usuários gerenciem o roteamento de tráfego de forma eficiente usando o kubectl. Segue o link da
documentação oficial do Kubernetes sobre o comando `iptables-save` para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#proxy-mode-iptables.

--NodePort
O NodePort é um tipo de serviço no Kubernetes que expõe um serviço em uma porta específica em cada nó do cluster Kubernetes. Ele permite que os usuários acessem
os serviços dentro do cluster Kubernetes de forma eficiente usando o kubectl, mesmo quando os serviços estão em nós diferentes dentro do cluster Kubernetes. O
NodePort é recomendado para casos em que os usuários desejam expor um serviço para o mundo externo, permitindo que os usuários acessem os serviços usando um
endereço IP do nó e a porta do NodePort, garantindo que os serviços sejam acessíveis de forma eficiente usando o kubectl. O NodePort é uma opção poderosa para
expor os serviços dentro do cluster Kubernetes para o mundo externo, permitindo que os usuários acessem os serviços de forma eficiente usando o kubectl. Segue o
link da documentação oficial do Kubernetes sobre NodePort para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#nodeport. O uso adequado do NodePort é fundamental para garantir a disponibilidade
e a confiabilidade dos serviços dentro do cluster Kubernetes, permitindo que os usuários acessem os serviços de forma eficiente usando o kubectl.
Se eu quiser alterar o meu serviço para o tipo NodePort, eu posso editar a configuração do serviço usando o comando `kubectl edit service <nome-do-serviço>`,
localizando a seção `type` e alterando o valor para `NodePort`, garantindo que o serviço seja exposto em uma porta específica em cada nó do cluster Kubernetes,
permitindo que os usuários acessem os serviços de forma eficiente usando o kubectl. É importante para garantir que as configurações sejam aplicadas, rebutando
ou excluindo os pods do serviço para que eles sejam recriados com as novas configurações, garantindo que o serviço seja exposto em uma porta específica em cada
nó do cluster Kubernetes, permitindo que os usuários acessem os serviços de forma eficiente usando o kubectl.

--LoadBalancer
O LoadBalancer é um tipo de serviço no Kubernetes que cria um balanceador de carga externo para expor os serviços dentro do cluster Kubernetes para o mundo
externo. Ele permite que os usuários acessam os serviços de forma eficiente usando o kubectl, mesmo quando os serviços estão em nós diferentes dentro do cluster
Kubernetes. O LoadBalancer é uma opção poderosa para expor os serviços dentro do cluster Kubernetes para o mundo externo, permitindo que os
usuários acessem os serviços de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre LoadBalancer para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer.
Quando esta rodando em cloud você não vai conseguir ver dados do cloud controller manager, mas se estiver rodando em bare metal, você pode usar o comando
`kubectl get service <nome-do-serviço> -o yaml` para verificar as informações do serviço, incluindo o endereço IP externo atribuído pelo balanceador de carga,
permitindo que os usuários verifiquem as informações do serviço e acessem os serviços de forma eficiente usando o kubectl. Se o serviço estiver rodando em um
ambiente de nuvem, como AWS, GCP ou Azure, o endereço IP externo atribuído pelo balanceador de carga pode ser verificado usando as ferramentas de gerenciamento
da nuvem, como o console de gerenciamento da AWS, o console do GCP ou o portal do Azure, permitindo que os usuários verifiquem as informações do serviço e
acessem os serviços de forma eficiente usando o kubectl e para mais informações: https://github.com/kubernetes/kubernetes/tree/v1.28.0/pkg/cloudprovider.
Abaixo segue um exemplo de configuração de Service do tipo LoadBalancer em um arquivo YAML para um Service do Kubernetes:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  ports:
    - port: 80
      targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```

Para rodar local é necessário usar uma ferramenta como o MetalLB, que é um balanceador de carga para ambientes de bare metal, permitindo que os usuários testem
e desenvolvam serviços do tipo LoadBalancer em um ambiente local usando o kubectl. O MetalLB é uma opção poderosa para rodar serviços do tipo LoadBalancer em um
ambiente local, permitindo que os usuários testem e desenvolvam serviços de forma eficiente usando o kubectl. Segue o link da documentação oficial do MetalLB
para mais informações: https://metallb.universe.tf/.

Para realizar a instalação do MetalLB, siga a documentação oficial do MetalLB: https://metallb.universe.tf/installation/#installation-by-manifest.
Após a instalação do MetalLB, é necessário configurar o pool de endereços IP para o MetalLB, basta seguir a documentação oficial do
MetalLb: https://metallb.universe.tf/configuration/#layer-2-configuration.
Para esse exemplo vamos criar um Layer 2 Configuration, que é uma configuração simples para ambientes de rede onde os nós do cluster Kubernetes estão na mesma
sub-rede, permitindo que o MetalLB atribua endereços IP diretamente aos serviços do tipo LoadBalancer, garantindo que os serviços sejam acessíveis de forma
eficiente usando o kubectl. Abaixo segue um exemplo de configuração de Layer 2 para o MetalLB em um arquivo YAML:

```yaml
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: private-subnet-pool
  namespace: metallb-system
spec:
  addresses:
    - 172.18.0.240-172.18.0.250
---
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: private-subnet-advertisement
  namespace: metallb-system
spec:
  ipAddressPools:
    - private-subnet-pool
```

O iprange passado em `addresses` deve ser o mesmo do internal-IP dos nodes, que podem ser acessados por `kubectl get node -owide` e o range deve ser pequeno,
para evitar conflitos de IPs, garantindo que os serviços do tipo LoadBalancer sejam acessíveis de forma eficiente usando o kubectl.

--Headless Service
Um Headless Service é um tipo de serviço no Kubernetes que não atribui um endereço IP para o serviço, permitindo que os usuários acessem os pods associados ao
serviço diretamente usando os nomes dos pods, em vez de usar um endereço IP do serviço. O Headless Service é recomendado para casos em que os usuários desejam
acessar os pods associados ao serviço diretamente, como em casos de bancos de dados ou outros aplicativos que exigem acesso direto aos pods, permitindo que os
usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre Headless Service para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#headless-services.

Abaixo segue um exemplo de configuração de Headless Service em um arquivo YAML para um Service do Kubernetes:

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  labels:
    app: nginx
  name: nginx-master
spec:
  serviceName: "nginx"
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

O StatefulSet acima cria 3 réplicas do nginx, cada uma com um volume persistente para armazenar os dados. O serviço associado a esse StatefulSet é um Headless
Service, que permite que os usuários acessem os pods diretamente usando os nomes dos pods, como `nginx-master-0`, `nginx-master-1` e `nginx-master-2`, em vez de
usar um endereço IP do serviço, garantindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Abaixo segue um exemplo de configuração de
Headless Service em um arquivo YAML para um Service do Kubernetes:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  selector:
    app: nginx
  ports:
    - name: https
      port: 80
      targetPort: 80
  type: ClusterIP
  clusterIP: None
```

--ExternalName
O ExternalName é um tipo de serviço no Kubernetes que mapeia um nome de serviço para um nome DNS externo, permitindo que os usuários acessem os recursos usando
um nome de domínio personalizado, em vez de usar um endereço IP do serviço. O ExternalName é recomendado para casos em que os usuários desejam acessar recursos
externos ao cluster Kubernetes usando um nome de domínio personalizado, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl.
Segue o link da documentação oficial do Kubernetes sobre ExternalName para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#externalname.
Abaixo segue um exemplo de configuração de ExternalName em um arquivo YAML para um Service do Kubernetes:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: blog
spec:
  type: ExternalName
  externalName: fillipefelixdev.com
```

--Trafic Policies
As políticas de tráfego no Kubernetes são um conjunto de regras e configurações que controlam como o tráfego é roteado e gerenciado dentro do cluster
Kubernetes. Elas permitem que os usuários definam regras para o roteamento de tráfego, balanceamento de carga, afinidade de pods e outras configurações
relacionadas ao tráfego, garantindo que os aplicativos e serviços dentro do cluster Kubernetes sejam acessíveis de forma eficiente.
As políticas de tráfego são recomendadas para casos em que os usuários desejam controlar o roteamento de tráfego e a distribuição de carga dentro do cluster
Kubernetes, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre
políticas de tráfego para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#traffic-policies.

--Canary Deployments
Os Canary Deployments são uma estratégia de implantação no Kubernetes que permite que os usuários implantem uma nova versão de um aplicativo ou serviço para um
pequeno subconjunto de usuários ou tráfego, permitindo que os usuários testem a nova versão em um ambiente de produção real antes de implantá-la para todos os
usuários. Os Canary Deployments são recomendados para casos em que os usuários desejam testar uma nova versão de um aplicativo ou serviço em um ambiente de
produção real, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre
Canary Deployments para mais
informações: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#canary-deployment.

Abaixo um exemplo de configuração de Deployment para um Canary `raiz` Deployment em um arquivo YAML para um Deployment do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-blue
  labels:
    app: nginx-blue
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          imagePullPolicy: Always
          image: nginx
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-green
  labels:
    app: nginx-green
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: httpd
          imagePullPolicy: Always
          image: httpd
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  ports:
    - port: 80
  selector:
    app: nginx
  type: LoadBalancer
```

--Blue-Green Deployments
Os Blue-Green Deployments são uma estratégia de implantação no Kubernetes que envolve a criação de duas versões do aplicativo ou serviço, uma versão "blue" e
uma versão "green". A versão "blue" é a versão atual do aplicativo ou serviço que está em produção, enquanto a versão "green" é a nova versão do aplicativo ou
serviço que está sendo testada. Os Blue-Green Deployments são recomendados para casos em que os usuários desejam implantar uma nova versão de um aplicativo ou
serviço com o mínimo de tempo de inatividade e risco, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da
documentação oficial do Kubernetes sobre Blue-Green Deployments para mais
informações: https://kubernetes.io/docs/concepts/services-networking/service/#blue-green-deployments.

Abaixo um exemplo de configuração de Deployment para um Blue-Green `raiz` Deployment em um arquivo YAML para um Deployment do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-blue
  labels:
    app: nginx-blue
spec:
  replicas: 10
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx-blue
    spec:
      containers:
        - name: nginx
          imagePullPolicy: Always
          image: nginx
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-green
  labels:
    app: nginx-green
spec:
  replicas: 10
  selector:
    matchLabels:
      app: nginx-green
  template:
    metadata:
      labels:
        app: nginx-green
    spec:
      containers:
        - name: httpd
          imagePullPolicy: Always
          image: httpd
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  ports:
    - port: 80
  selector:
    app: nginx-green
  type: ClusterIP
```

--Ingress
O Ingress é um recurso do Kubernetes que permite que os usuários exponham os serviços dentro do cluster Kubernetes para o mundo externo, permitindo que os
usuários acessem os serviços usando um nome de domínio personalizado, em vez de usar um endereço IP do serviço. O Ingress é recomendado para casos em que os
usuários desejam expor os serviços para o mundo externo usando um nome de domínio personalizado, permitindo que os usuários acessem os serviços de forma
eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre Ingress para mais
informações: https://kubernetes.io/docs/concepts/services-networking/ingress/.

Em `docs/examplos-k8s/ingress` tem um exemplo de configuração de Ingress em um arquivo YAML para um Ingress do Kubernetes, que inclui a configuração de um
controlador de Ingress, regras de roteamento e um serviço associado para expor os serviços dentro do cluster Kubernetes para o mundo externo usando o kubectl.
Para configurar o ingressclass e deixar um como padrão, basta usar o comando `kubectl edit ingressclass nginx` e adicionar a linha em annotations
`ingressclass.kubernetes.io/is-default-class: "true"`, garantindo que o controlador de Ingress seja configurado como o controlador de Ingress padrão para o
cluster Kubernetes, permitindo que os usuários exponham os serviços para o mundo externo usando um nome de domínio personalizado, em vez de usar um endereço IP
do serviço, garantindo que os usuários acessem os serviços de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre
IngressClass para mais informações: https://kubernetes.io/docs/concepts/services-networking/ingress/#ingress-class.

--Ingress Resource
O Ingress Resource é um recurso do Kubernetes que define as regras de roteamento para o tráfego de entrada para os serviços dentro do cluster Kubernetes. Ele
permite que os usuários definam regras para o roteamento de tráfego com base em host, caminho e outras condições, garantindo que os serviços dentro do cluster
Kubernetes sejam acessíveis de forma eficiente. O Ingress Resource é recomendado para casos em que os usuários desejam controlar o
roteamento de tráfego de entrada para os serviços dentro do cluster Kubernetes, permitindo que os usuários acessem os serviços de forma eficiente usando o
kubectl. Segue o link da documentação oficial do Kubernetes sobre Ingress Resource para mais
informações: https://kubernetes.io/docs/concepts/services-networking/ingress/#the-ingress-resource.

Abaixo um exemplo de configuração de Ingress Resource em um arquivo YAML para um Ingress do Kubernetes:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: web-service-ingress
spec:
  ingressClassName: nginx # Nome do controlador de Ingress a ser usado
  rules:
    - host: nginx.demo.com
    - http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx
                port:
                  number: 80
```

O Ingress Resource acima define uma regra de roteamento para o tráfego de entrada para o serviço `nginx` com base no host `nginx.demo.com` e no caminho `/`,
garantindo que os usuários acessem os serviços de forma eficiente usando o kubectl.

--Ingress Classes (Multiplos controladores de Ingress)
As Ingress Classes são um recurso do Kubernetes que permite que os usuários definam diferentes classes de Ingress para controlar o roteamento de tráfego de
entrada para os serviços dentro do cluster Kubernetes. Elas permitem que os usuários definam diferentes controladores de Ingress para diferentes classes de
Ingress, garantindo que os serviços dentro do cluster Kubernetes sejam acessíveis de forma eficiente.
Para utilizar o multiplos controladores vamos utilizar o traefik como controlador de Ingress, que é um controlador de Ingress popular e amplamente utilizado no
Kubernetes, permitindo que os usuários controlem o roteamento de tráfego de entrada para os serviços dentro do cluster Kubernetes usando o kubectl. O Traefik é
recomendado para casos em que os usuários desejam usar um controlador de Ingress alternativo para controlar o roteamento de tráfego de entrada para os serviços
dentro do cluster Kubernetes, permitindo que os usuários acessem os serviços de forma eficiente usando o kubectl. Segue o link da documentação oficial do
Traefik para mais informações: https://doc.traefik.io/traefik/getting-started/install-traefik/#use-the-helm-chart.
Primeiro é necessário instalar o Traefik usando o Helm, que é um gerenciador de pacotes para Kubernetes, permitindo que os usuários instalem e gerenciem o
Traefik de forma eficiente usando o kubectl. Para instalar o Traefik usando o Helm, siga os passos abaixo:

1. Adicione o repositório do Traefik ao Helm usando o comando `helm repo add traefik https://helm.traefik.io/traefik`, garantindo que o repositório do Traefik
   seja adicionado ao Helm para que os usuários possam instalar o Traefik usando o kubectl.
2. Atualize o repositório do Helm usando o comando `helm repo update`, garantindo que o repositório do Traefik seja atualizado para que os usuários possam
   instalar a versão mais recente do Traefik usando o kubectl.
3. Instale o Traefik usando o comando `helm install traefik traefik/traefik --namespace traefik --create-namespace --set logs.access.enable=true`, garantindo
   que o Traefik seja instalado no namespace `traefik` com os logs de acesso habilitados, permitindo que os usuários controlem o roteamento de tráfego de
   entrada
   para os serviços dentro do cluster Kubernetes usando o kubectl.
4. Após a instalação do Traefik, é necessário configurar o IngressClass para o Traefik, basta usar o comando `kubectl apply -f <arquivo-ingressclass>.yaml` para
   aplicar a configuração do IngressClass para o Traefik, garantindo que o controlador de Ingress do Traefik seja configurado corretamente para controlar o
   roteamento de tráfego de entrada para os serviços dentro do cluster Kubernetes usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre
   IngressClass para mais informações: https://kubernetes.io/docs/concepts/services-networking/ingress/#ingress-class.

Abaixo um exemplo de configuração de Ingress Class para o Traefik em um arquivo YAML para um Ingress do Kubernetes:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: web-service-ingress
spec:
  ingressClassName: traefik # Nome do controlador de Ingress a ser usado
  rules:
    - host: nginx.demo.com
    - http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx
                port:
                  number: 80
```

--Multiples services no mesmo Ingress
É possível configurar múltiplos serviços no mesmo Ingress no Kubernetes, permitindo que os usuários controlem o roteamento de tráfego de entrada para vários
serviços dentro do cluster Kubernetes usando um único recurso de Ingress, garantindo que os serviços sejam acessíveis de forma eficiente e confiável usando o
kubectl. Para configurar múltiplos serviços no mesmo Ingress, basta definir múltiplas regras de roteamento no recurso de Ingress, cada uma apontando para um
serviço diferente, garantindo que os usuários controlem o roteamento de tráfego de entrada para vários serviços dentro do cluster Kubernetes usando o kubectl.
Segue o link da documentação oficial do Kubernetes sobre Ingress para mais
informações: https://kubernetes.io/docs/concepts/services-networking/ingress/#the-ingress-resource.
Abaixo um exemplo de configuração de múltiplos serviços no mesmo Ingress em um arquivo YAML para um Ingress do Kubernetes:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: web-service-ingress
spec:
  ingressClassName: nginx # Nome do controlador de Ingress a ser usado
  rules:
    - host: nginx.demo.com
    - http:
        paths:
          - path: /nginx
            pathType: Prefix
            backend:
              service:
                name: nginx
                port:
                  number: 80
    - http:
        paths:
          - path: /httpd
            pathType: Prefix
            backend:
              service:
                name: httpd
                port:
                  number: 80
```

--ConfigMaps e Secrets
Os ConfigMaps e Secrets são recursos do Kubernetes que permitem que os usuários armazenem e gerenciem informações de configuração e dados sensíveis dentro do
cluster Kubernetes. Os ConfigMaps são usados para armazenar informações de configuração não sensíveis, como variáveis de ambiente, arquivos de configuração e
outros dados de configuração, enquanto os Secrets são usados para armazenar informações sensíveis, como senhas, chaves de API e outros dados confidenciais. Os
ConfigMaps e Secrets são recomendados para casos em que os usuários desejam armazenar e gerenciar informações de configuração e dados sensíveis dentro do
cluster Kubernetes, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre
ConfigMaps e Secrets para mais
informações: https://kubernetes.io/docs/concepts/configuration/configmap/ e https://kubernetes.io/docs/concepts/configuration/secret/.
Abaixo um exemplo de configuração de ConfigMap e Secret em um arquivo YAML para um ConfigMap e um Secret do Kubernetes:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-demo
data:
  virual_host: "vhost1.localhost.com"
  index.html: |
    <html>
    <head>
        <title>ConfigMap Example</title>
    </head>
    <body>
    <h1>ConfigMap Example</h1>
    <p>This is an example of a ConfigMap in Kubernetes.</p>
    </body>
    </html>
  vhost.conf: |
    server {
        listen 80;
        listen [::]:80;

        root /usr/share/nginx/app1;
        index index.html index.htm index.nginx-debian.html;

        server_name app.localhost.com www.app.localhost.com;

        location / {
            try_files $uri $uri/ =404;
        }
    }
---
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
            - name: VIRTUAL_HOST
              valueFrom:
                configMapKeyRef:
                  name: nginx-demo
                  key: virual_host
          volumeMounts:
            - mountPath: /usr/share/nginx/app1/index.html
              subPath: index.html
              name: index-html
            - mountPath: /etc/nginx/conf.d/vhost.conf
              subPath: vhost.conf
              name: vhost
      volumes:
        - name: index-html
          configMap:
            name: nginx-demo
            items:
              - key: index.html
                path: index.html
        - name: vhost
          configMap:
            name: nginx-demo
            items:
              - key: vhost.conf
                path: vhost.conf
```

O ConfigMap acima define duas chaves, `index.html` e `vhost.conf`, que contêm o conteúdo do arquivo HTML e do arquivo de configuração do Nginx, respectivamente.
O Deployment do Nginx monta o arquivo `index.html` do ConfigMap no caminho `/usr/share/nginx/app1/index.html` dentro do contêiner usando a diretiva `subPath`, e
o arquivo `vhost.conf` do ConfigMap é montado no caminho `/etc/nginx/conf.d/vhost.conf` dentro do contêiner usando a diretiva `subPath`, garantindo que os
usuários acessem os recursos de forma eficiente usando o kubectl. A diretiva subPath é usada para montar apenas o arquivo `index.html` do ConfigMap no caminho
especificado dentro do contêiner, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl.

--Secrets
Os Secrets são usados para armazenar informações sensíveis, como senhas, chaves de API e outros dados confidenciais, garantindo que os usuários acessem os
recursos de forma eficiente usando o kubectl. Os Secrets são recomendados para casos em que os usuários desejam armazenar e gerenciar informações sensíveis
dentro do cluster Kubernetes, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl. Segue o link da documentação oficial do
Kubernetes sobre Secrets para mais informações: https://kubernetes.io/docs/concepts/configuration/secret/.
Abaixo um exemplo de configuração de Secret em um arquivo YAML para um Secret do Kubernetes:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: credentials
type: kunernetes.io/basic-auth
data:
  username: bWF0ZXVz
  password: bWF0ZXVz
---
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
            - name: USERNAME
              valueFrom:
                secretKeyRef:
                  name: credentials
                  key: username
            - name: PASSWORD
              valueFrom:
                secretKeyRef:
                  name: credentials
                  key: password
          volumeMounts:
            - mountPath: /tmp
              name: credentials
              readOnly: true
      volumes:
        - name: credentials
          secret:
            secretName: credentials
```

O Secret acima define duas chaves, `username` e `password`, que contêm as credenciais codificadas em base64. O Deployment do Nginx monta o Secret como um volume
no caminho `/tmp` dentro do contêiner, garantindo que os usuários acessem os recursos de forma eficiente usando o kubectl. As variáveis de ambiente `USERNAME` e
`PASSWORD` são definidas usando a diretiva `valueFrom` para referenciar as chaves do Secret, permitindo que os usuários acessem os recursos de forma eficiente
usando o kubectl. O Secret é montado como um volume no caminho `/tmp` dentro do contêiner, garantindo que os usuários acessem os recursos de forma eficiente
usando o kubectl. O tipo do Secret é definido como `kubernetes.io/basic-auth`, indicando que o Secret contém credenciais de autenticação básica, garantindo que
os usuários acessem os recursos de forma eficiente usando o kubectl.

--Comandos para configMaps e Secrets

`kubectl create configmap <nome-do-configmap> --from-literal=<chave>=<valor>`: Cria um ConfigMap a partir de um par chave-valor, permitindo que os usuários
criem ConfigMaps de forma rápida e eficiente usando o kubectl.
`kubectl create secret generic <nome-do-secret> --from-literal=<chave>=<valor>`: Cria um Secret a partir de um par chave-valor, permitindo que os usuários criem
Secrets de forma rápida e eficiente usando o kubectl.
`kubectl get configmap <nome-do-configmap> -o yaml`: Exibe as informações de um ConfigMap em formato YAML, permitindo que os usuários verifiquem as informações
de configuração armazenadas em um ConfigMap usando o kubectl.
`kubectl get secret <nome-do-secret> -o yaml`: Exibe as informações de um Secret em formato YAML, permitindo que os usuários verifiquem as informações sensíveis
armazenadas em um Secret usando o kubectl.
`kubectl edit configmap <nome-do-configmap>`: Edita um ConfigMap usando um editor de texto, permitindo que os usuários modifiquem as informações de configuração
armazenadas em um ConfigMap de forma eficiente usando o kubectl.
`kubectl edit secret <nome-do-secret>`: Edita um Secret usando um editor de texto, permitindo que os usuários modifiquem as informações sensíveis armazenadas em
um Secret de forma eficiente usando o kubectl.
`kubectl delete configmap <nome-do-configmap>`: Exclui um ConfigMap, permitindo que os usuários removam informações de configuração armazenadas em um ConfigMap
usando o kubectl.
`kubectl delete secret <nome-do-secret>`: Exclui um Secret, permitindo que os usuários removam informações sensíveis armazenadas em um Secret usando o kubectl.
Segue o link da documentação oficial do Kubernetes sobre comandos para ConfigMaps e Secrets para mais
informações: https://kubernetes.io/docs/concepts/configuration/configmap/#create-a-configmap-from-literal-values
e https://kubernetes.io/docs/concepts/configuration/secret/#create-a-secret-from-literal-values.

--Storage no Kubernetes
O armazenamento no Kubernetes é um componente fundamental para garantir a persistência dos dados e a disponibilidade dos aplicativos e serviços dentro do
cluster Kubernetes. O Kubernetes oferece diferentes opções de armazenamento, como Persistent Volumes (PVs), Persistent Volume Claims (PVCs) e Storage Classes,
permitindo que os usuários escolham a melhor opção de armazenamento para suas necessidades específicas, garantindo que os dados sejam armazenados de forma
eficiente. O armazenamento no Kubernetes é recomendado para casos em que os usuários desejam garantir a persistência dos dados e a
disponibilidade dos aplicativos e serviços dentro do cluster Kubernetes, permitindo que os usuários acessem os recursos de forma eficiente usando o kubectl.
Segue o link da documentação oficial do Kubernetes sobre armazenamento para mais
informações: https://kubernetes.io/docs/concepts/storage/.
Abaixo uma visão geral dos principais recursos de armazenamento no Kubernetes:

- Os **Persistent Volumes (PVs)** são recursos do Kubernetes que representam uma parte do armazenamento físico disponível no cluster Kubernetes, permitindo que
  os usuários provisionem e gerenciem o armazenamento de forma eficiente usando o kubectl. Os PVs são recomendados para casos em que os usuários desejam
  provisionar e gerenciar o armazenamento de forma eficiente dentro do cluster Kubernetes, garantindo que os dados sejam armazenados de forma confiável usando o
  kubectl. O PV é o storage que vai ser disponibilizado para os usuários no cluster, é a parte de infra. Segue o link da documentação oficial do Kubernetes
  sobre Persistent Volumes para mais informações: https://kubernetes.io/docs/concepts/storage/persistent-volumes/.
- Os **Persistent Volume Claims (PVCs)** são recursos do Kubernetes que representam uma solicitação de armazenamento feita por um usuário ou aplicativo dentro
  do cluster Kubernetes, permitindo que os usuários solicitem e gerenciem o armazenamento de forma eficiente usando o kubectl. Os PVCs são recomendados para
  casos em que os usuários desejam solicitar e gerenciar o armazenamento de forma eficiente dentro do cluster Kubernetes, garantindo que os dados sejam
  armazenados de forma confiável usando o kubectl. Normalmente o pod não se comunica diretamente com o PV, ele se comunica diretamente como PVC, que seria como
  se fosse um pedaço do PVC. Onde cada aplicação vai ter um PVC atrelado para pedir o pedaço do storage que seria o PV. Segue o link da documentação oficial do
  Kubernetes sobre Persistent Volume Claims para mais informações: https://kubernetes.io/docs/concepts/storage/persistent-volume-claims/.
- As **Storage Classes** são recursos do Kubernetes que definem as classes de armazenamento disponíveis no cluster Kubernetes, permitindo que os usuários
  escolham a melhor opção de armazenamento para suas necessidades específicas, garantindo que os dados sejam armazenados de forma eficiente e confiável usando o
  kubectl. As Storage Classes são recomendadas para casos em que os usuários desejam escolher a melhor opção de armazenamento para suas necessidades específicas
  dentro do cluster Kubernetes, garantindo que os dados sejam armazenados de forma eficiente. É como se fosse uma prateleira de
  storages disponiveis, onde você pode escolher qual deles você vai poder utilizar. Segue o link da documentação oficial
  do Kubernetes sobre Storage Classes para mais informações: https://kubernetes.io/docs/concepts/storage/storage-classes/.

Abaixo um exemplo de configuração de Persistent Volume, Persistent Volume Claim em um arquivo YAML para um Persistent Volume, Persistent
Volume Claim do Kubernetes:

PV

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: example-pv
spec:
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  local:
    path: /data
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: kubernetes.io/hostname
              operator: In
              values:
                - comunidade-devops-worker
```

PVC

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  volumeMode: Filesystem
  resources:
    requests:
      storage: 1Gi
  storageClassName: "" # Deixando em branco para usar o PV sem StorageClass
  volumeName: example-pv # Especificando o nome do PV para vincular diretamente
```

Deploy usando PVC

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
  name: nginx
  namespace: default
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
          volumeMounts:
            - mountPath: /data # Caminho dentro do container onde o volume será montado
              name: local # Referenciando o nome do volume definido na seção de volumes
      volumes:
        - name: local # Nome do volume a ser referenciado no container
          persistentVolumeClaim:
            claimName: myclaim # Especificando o nome do PVC para montar o volume
```

O exemplo acima define um Persistent Volume (PV) chamado `example-pv` com uma capacidade de 5Gi, acesso do tipo ReadWriteOnce e um caminho local para
armazenamento. O Persistent Volume Claim (PVC) chamado `myclaim` solicita 1Gi de armazenamento, com acesso do tipo ReadWriteOnce, e está vinculado diretamente
ao PV `example-pv` sem usar uma Storage Class. O Deployment do Nginx monta o PVC `myclaim` no caminho `/data` dentro do contêiner, garantindo que os dados sejam
armazenados no kubectl. O PV é configurado para ser acessível apenas pelo nó `comunidade-devops-worker`, garantindo que os
dados sejam armazenados de forma eficiente.

Agora vou mostrar um exemplo de configuração de Storage Class (Dynamic Volume) em um arquivo YAML para uma Storage Class do Kubernetes:

PVC

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  volumeMode: Filesystem
  resources:
    requests:
      storage: 1Gi
  storageClassName: "local-path" # Substitua pelo nome da StorageClass que deseja usar
```

Deploy usando PVC

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
  name: nginx-deployment
  namespace: default
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
          volumeMounts:
            - mountPath: /data # Caminho dentro do container onde o volume será montado
              name: local # Referenciando o nome do volume definido na seção de volumes
      volumes:
        - name: local # Nome do volume a ser referenciado no container
          persistentVolumeClaim:
            claimName: myclaim # Especificando o nome do PVC para montar o volume
```

O exemplo acima define um Persistent Volume Claim (PVC) chamado `myclaim` que solicita 1Gi de armazenamento, com acesso do tipo ReadWriteOnce, e está vinculado
a uma Storage Class chamada `local-path`. O Deployment do Nginx monta o PVC `myclaim` no caminho `/data` dentro do contêiner, garantindo que os dados sejam
armazenados de forma eficiente. A Storage Class `local-path` é um exemplo de Storage Class que pode ser usada para provisionamento
dinâmico de volumes locais, permitindo que os usuários criem volumes de forma dinâmica com base nas solicitações de armazenamento feitas pelos PVCs, garantindo
que os dados sejam armazenados de forma eficiente. Segue o link da documentação oficial do Kubernetes sobre Storage Classes para
mais informações: https://kubernetes.io/docs/concepts/storage/storage-classes/.
Essa é uma das vantagens de usar o privisionamento dinâmico de volumes com Storage Classes, onde os usuários podem criar volumes de forma dinâmica com base nas
solicitações de armazenamento feitas pelos PVCs, sem a necessidade de criar PVs manualmente, e o controlador de provisionamento dinâmico do Kubernetes se
encarrega de criar os PVs automaticamente com base nas solicitações dos PVCs e configurar os diretorios necessarios, os permissionamentos e o que for necessário
para garantir que os dados sejam armazenados. Dessa forma fica tudo muito mais automatizado e eficiente, permitindo que os usuários acessem os recursos de forma
eficiente usando o kubectl.

--Access Modes
Os Access Modes são um recurso do Kubernetes que define os modos de acesso para os volumes persistentes dentro do cluster Kubernetes, permitindo que os usuários
controlem como os volumes são acessados pelos pods e aplicativos dentro do cluster Kubernetes, garantindo que os dados sejam armazenados de forma eficiente e
confiável usando o kubectl. Os Access Modes são recomendados para casos em que os usuários desejam controlar como os volumes persistentes são acessados pelos
pods e aplicativos dentro do cluster Kubernetes, garantindo que os dados sejam armazenados de forma eficiente. Segue o link da
documentação oficial do Kubernetes sobre Access Modes para mais informações: https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes.
Abaixo uma visão geral dos principais Access Modes no Kubernetes:

- **ReadWriteOnce (RWO)**: Permite que um volume seja montado como leitura e escrita por um único nó(node), ainda pode que varios pods acessem o mesmo volume,
  desde que eles estejam rodando no mesmo node.
- **ReadOnlyMany (ROX)**: Permite que um volume seja montado como somente leitura por vários nós(nodes), garantindo que os dados sejam acessados de forma
  eficiente. O Access Mode ReadOnlyMany é recomendado para casos em que os usuários desejam garantir que um volume seja montado
  como somente leitura por vários nós dentro do cluster Kubernetes, garantindo que os dados sejam acessados de forma eficiente.
- **ReadWriteMany (RWX)**: Permite que um volume seja montado como leitura e escrita por vários nós, garantindo que os dados sejam acessados de forma eficiente
  . O Access Mode ReadWriteMany é recomendado para casos em que os usuários desejam garantir que um volume seja montado como leitura
  e escrita por vários nós dentro do cluster Kubernetes, garantindo que os dados sejam acessados de forma eficiente.
- **ReadWriteOncePod (RWOP)**: Permite que um volume seja montado como leitura e escrita por um único pod, garantindo que os dados sejam acessados de forma
  eficiente. O Access Mode ReadWriteOncePod é recomendado para casos em que os usuários desejam garantir que um volume seja montado
  como leitura e escrita por um único pod dentro do cluster Kubernetes, garantindo que os dados sejam acessados de forma eficiente.

--Reclaim Policy
A Reclaim Policy é um recurso do Kubernetes que define a política de recuperação para os volumes persistentes dentro do cluster Kubernetes, permitindo que os
usuários controlem o que acontece com os volumes persistentes quando eles são liberados pelos pods ou aplicativos dentro do cluster Kubernetes, garantindo que
os dados sejam armazenados de forma eficiente. A Reclaim Policy é recomendada para casos em que os usuários desejam controlar o que
acontece com os volumes persistentes quando eles são liberados pelos pods ou aplicativos dentro do cluster Kubernetes, garantindo que os dados sejam armazenados
de forma eficiente. Segue o link da documentação oficial do Kubernetes sobre Reclaim Policy para mais
informações: https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaim-policy.
Abaixo uma visão geral dos principais Reclaim Policies no Kubernetes:

- **Retain**: A política de recuperação Retain mantém o volume persistente mesmo após ele ser liberado pelos pods ou aplicativos, garantindo que os dados sejam
  preservados e possam ser recuperados posteriormente usando o kubectl. A Reclaim Policy Retain é recomendada para casos em que os usuários desejam garantir que
  um volume persistente seja mantido mesmo após ser liberado pelos pods ou aplicativos dentro do cluster Kubernetes, garantindo que os dados sejam preservados
  e possam ser recuperados posteriormente usando o kubectl.
- **Delete**: A política de recuperação Delete exclui o volume persistente quando ele é liberado pelos pods ou aplicativos, garantindo que os dados sejam
  removidos de forma eficiente. A Reclaim Policy Delete é recomendada para casos em que os usuários desejam garantir que um volume
  persistente seja excluído quando ele for liberado pelos pods ou aplicativos dentro do cluster Kubernetes, garantindo que os dados sejam removidos de forma
  eficiente.
- **Recycle**: A política de recuperação Recycle limpa o volume persistente e o torna disponível para reutilização quando ele é liberado pelos pods ou
  aplicativos, garantindo que os dados sejam removidos de forma eficiente. A Reclaim Policy Recycle é recomendada para casos em que
  os usuários desejam garantir que um volume persistente seja limpo e reutilizado quando ele for liberado pelos pods ou aplicativos dentro do cluster
  Kubernetes, garantindo que os dados sejam removidos de forma eficiente. Atualmente a Reclaim Policy Recycle está obsoleta e não é
  mais recomendada para uso, sendo substituída por outras opções de recuperação, como Retain ou Delete, para garantir que os dados sejam gerenciados de forma
  eficiente.

--Projected Volumes
Os Projected Volumes são um recurso do Kubernetes que permite que os usuários projetem múltiplos volumes em um único volume dentro do cluster Kubernetes,
permitindo que os usuários combinem diferentes fontes de dados, como ConfigMaps, Secrets e Downward API, em um único volume para ser montado pelos pods e
aplicativos dentro do cluster Kubernetes, garantindo que os dados sejam acessados de forma eficiente. Os Projected Volumes são
recomendados para casos em que os usuários desejam combinar diferentes fontes de dados em um único volume para ser montado pelos pods e aplicativos dentro do
cluster Kubernetes, garantindo que os dados sejam acessados de forma eficiente. Segue o link da documentação oficial do Kubernetes
sobre Projected Volumes para mais informações: https://kubernetes.io/docs/concepts/storage/projected-volumes/.
Abaixo um exemplo de configuração de Projected Volume em um arquivo YAML para um Projected Volume do Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
  name: nginx-deployment
  namespace: default
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
          volumeMounts:
            - mountPath: /tmp # Caminho onde os arquivos do volume serão montados no container
              name: all-in-one # Nome do volume a ser referenciado no container
      volumes:
        - name: all-in-one # Nome do volume a ser referenciado no container
          projected:
            sources:
              - configMap:
                  name: nginx-demo
                  items:
                    - key: index.html
                      path: index.html
                    - key: vhost.conf
                      path: vhost.conf
                    - key: virual_host
                      path: virual_host
              - secret:
                  name: credentials
                  items:
                    - key: username
                      path: creds/username
                    - key: password
                      path: creds/password
```

O exemplo acima define um Deployment do Nginx que monta um Projected Volume chamado `all-in-one` no caminho `/tmp` dentro do contêiner. O Projected Volume
combinadados de um ConfigMap chamado `nginx-demo` e um Secret chamado `credentials`, permitindo que os arquivos `index.html`, `vhost.conf` e `virual_host` do
ConfigMap, bem como as chaves `username` e `password` do Secret, sejam montados em um único volume para ser acessado pelo contêiner.

--Autoscaling no Kubernetes
O Autoscaling no Kubernetes é um recurso que permite que os usuários configurem a escalabilidade automática para os pods e aplicativos dentro do cluster
Kubernetes. Autoscaling no Kubernetes (K8s) é quando o cluster
aumenta ou diminui recursos automaticamente, sem você precisar fazer isso manualmente. Segue o link da documentação oficial do Kubernetes sobre Autoscaling para
mais informações: https://kubernetes.io/docs/concepts/workloads/autoscaling/.
Existe diferentes tipos de Autoscaling no Kubernetes, como Horizontal Pod Autoscaler (HPA), Vertical Pod Autoscaler (VPA) e Cluster Autoscaler, permitindo que
os usuários escolham a melhor opção de escalabilidade automática para suas necessidades específicas, garantindo que osrecursos sejam alocados de forma eficiente
e confiável usando o kubectl. Abaixo uma visão geral dos principais tipos de Autoscaling no Kubernetes:

- **Horizontal Pod Autoscaler (HPA)**: O HPA é um recurso do Kubernetes que permite que os usuários configurem a escalabilidade automática horizontal para os
  pods dentro do cluster Kubernetes. O HPA é recomendado para casos em que os usuários desejam configurar a escalabilidade automática horizontal para os pods
  dentro do cluster Kubernetes. O HPA monitora métricas como CPU, memória ou outras métricas personalizadas para ajustar automaticamente o número de réplicas
  dos pods. Para mais informações sobre o HPA, siga o link da documentação oficial do Kubernetes sobre Horizontal Pod
  Autoscaler: https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale/.
- **Vertical Pod Autoscaler (VPA)**: O VPA é um recurso do Kubernetes que permite que os usuários configurem a escalabilidade automática vertical para os pods
  dentro do cluster Kubernetes. O VPA é recomendado para casos em que os usuários desejam configurar a escalabilidade automática vertical para os pods dentro do
  cluster Kubernetes. O VPA ajusta automaticamente os recursos de CPU e memória dos pods com base nas necessidades de carga. Para mais informações sobre o VPA,
  siga o link da documentação oficial do Kubernetes sobre Vertical Pod
  Autoscaler: https://kubernetes.io/docs/concepts/workloads/autoscaling/vertical-pod-autoscale/.

Um ponto importante é que é necessario ter o metrics-server instalado no cluster Kubernetes para que o HPA e o VPA possam coletar as métricas necessárias para
ajustar a escalabilidade automática dos pods. O metrics-server é um componente do Kubernetes que coleta métricas de recursos, como CPU e memória, dos pods e nós
dentro do cluster Kubernetes, permitindo que o HPA e o VPA ajustem automaticamente a escalabilidade dos pods com base nas necessidades de carga. Para instalar o
metrics-server no cluster Kubernetes, siga os passos a passos do link https://github.com/kubernetes-sigs/metrics-server.

Abaixo um exemplo de configuração de Horizontal Pod Autoscaler (HPA) em um arquivo YAML para um HPA do Kubernetes:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-hpa
spec:
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300 # O tempo que o HPA vai esperar para escalar para baixo, ou seja, para reduzir o numero de replicas, depois que a utilização do recurso voltar a ficar abaixo do limite definido, nesse caso 60% de utilização da CPU, para evitar que o HPA fique escalando para baixo e para cima rapidamente, causando instabilidade no cluster
      policies:
        - type: Percent
          value: 100 # O valor máximo que o HPA pode reduzir o numero de replicas em um periodo de tempo, nesse caso 100% ou seja, ele pode reduzir o numero de replicas para 0 em um periodo de tempo, mas como o numero minimo de replicas é 1, ele não vai reduzir para 0
          periodSeconds: 300 # O periodo de tempo que o HPA vai levar em consideração para aplicar a politica de redução do numero de replicas, nesse caso 300 segundos ou seja, 5 minutos
  metrics: # As metricas que vai levar em consideração para escalar o deployment, nesse caso a utilização da CPU
    - resource:
        name: cpu
        target:
          averageUtilization: 60
          type: Utilization
      type: Resource
  minReplicas: 1
  maxReplicas: 100 # Importante colocar um numero maximo de replicas para evitar que o HPA escale demais o deployment e acabe causando problemas no cluster
  scaleTargetRef: # O deployment que o HPA vai escalar, nesse caso o deployment do nginx
    apiVersion: apps/v1
    kind: Deployment
    name: nginx
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 1 # Esse numero de replicas geralmente não vai ser usada quando utilizamos o HPA, pois ele vai escalar o numero de replicas de acordo com a utilização do recurso, mas é importante colocar um numero inicial para o HPA ter uma base para escalar
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
          resources:
            requests: # Esse ponto é importante para o HPA, pois ele precisa saber qual é a utilização atual do recurso para poder escalar
              cpu: 10m
            limits:
              cpu: 100m
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  ports:
    - port: 80
  selector:
    app: nginx
  type: ClusterIP
```

Uma forma para poder testar o HPA é utilizando a ferramenta `kubectl run` para criar uma carga de trabalho artificial no cluster Kubernetes, permitindo que os
usuários testem a escalabilidade automática do HPA de forma eficiente usando o kubectl. Para criar uma carga de trabalho artificial usando o `kubectl run`,
basta usar o comando `kubectl run -it --image=alpine demo2 --rm sh` para criar um pod interativo com a imagem do alpine, e em seguida usar o
comando `while true; do curl nginx; done` dentro do pod para gerar uma carga de trabalho contínua no cluster Kubernetes, permitindo que os
usuários testem a escalabilidade automática do HPA de forma eficiente usando o kubectl. Em outro terminal você pode usar o comando `kubectl get hpa -w` para
verificar se o HPA está escalando o número de réplicas do deployment do nginx de acordo com a carga de trabalho gerada, garantindo que os dados sejam
armazenados de forma eficiente usando o kubectl.

--Comandos para HPA
`kubectl get hpa`: Exibe a lista de Horizontal Pod Autoscalers (HPAs) no cluster Kubernetes, permitindo que os usuários verifiquem os HPAs configurados usando o
kubectl.
`kubectl describe hpa <nome-do-hpa>`: Exibe detalhes sobre um Horizontal Pod Autoscaler específico, incluindo as métricas monitoradas, o número de réplicas
atuais
e o número de réplicas desejadas, permitindo que os usuários verifiquem as informações detalhadas sobre um HPA específico usando o kubectl.
`kubectl edit hpa <nome-do-hpa>`: Edita um Horizontal Pod Autoscaler usando um editor de texto, permitindo que os usuários modifiquem as configurações de um HPA
específico de forma eficiente usando o kubectl.
`kubectl delete hpa <nome-do-hpa>`: Exclui um Horizontal Pod Autoscaler, permitindo que os usuários removam um HPA específico do cluster Kubernetes usando o
kubectl.

--CNI no Kubernetes
O CNI (Container Network Interface) é um recurso do Kubernetes que define a interface de rede para os contêineres dentro do cluster Kubernetes, permitindo que
os usuários configurem e gerenciem a rede de forma eficiente usando o kubectl. O CNI é recomendado para casos em que os usuários desejam configurar e gerenciar
a rede de forma eficiente dentro do cluster Kubernetes, garantindo que os dados sejam transmitidos de forma eficiente usando o kubectl. Segue o link da
documentação oficial do Kubernetes sobre CNI para mais
informações: https://kubernetes.io/docs/concepts/cluster-administration/networking/.
O CNI é um padrão de interface de rede para contêineres que permite que os usuários configurem e gerenciem a rede de forma eficiente dentro do cluster
Kubernetes, garantindo que os dados sejam transmitidos de forma eficiente usando o kubectl. O CNI é um conjunto de especificações e bibliotecas que permitem que
os plugins de rede sejam integrados ao Kubernetes, permitindo que os usuários escolham a melhor opção de plugin de rede para suas necessidades específicas,
garantindo que os dados sejam transmitidos de forma eficiente usando o kubectl. Existem diferentes plugins de rede compatíveis com o CNI, como Calico, Flannel,
Weave Net, Cilium, entre outros, permitindo que os usuários escolham a melhor opção de plugin de rede para suas necessidades específicas, garantindo que os
dados sejam transmitidos de forma eficiente usando o kubectl. Para mais informações sobre os plugins de rede compatíveis com o CNI, siga o link da documentação
oficial do Kubernetes sobre plugins de rede compatíveis com o
CNI: https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/.

--Como funciona a intercomunicação pela CNI com o Flannel
O Flannel é um plugin de rede compatível com o CNI que permite que os contêineres dentro do cluster Kubernetes se comuniquem entre si de forma eficiente usando
o kubectl. O Flannel funciona criando uma rede virtual sobre a rede física do cluster Kubernetes, permitindo que os contêineres se comuniquem entre si usando
endereços IP virtuais, garantindo que os dados sejam transmitidos de forma eficiente usando o kubectl. Para mais informações sobre o Flannel, siga o link da
documentação oficial sobre Flannel: https://github.com/flannel-io/flannel.

--Network Policies no Kubernetes
As Network Policies são um recurso do Kubernetes que permite que os usuários controlem o tráfego de rede entre os pods e aplicativos dentro do cluster
Kubernetes, garantindo que os dados sejam transmitidos de forma eficiente usando o kubectl. As Network Policies são recomendadas para casos em que os usuários
desejam controlar o tráfego de rede entre os pods e aplicativos dentro do cluster Kubernetes, garantindo que os dados sejam transmitidos de forma eficiente
usando o kubectl. Segue o link da documentação oficial do Kubernetes sobre Network Policies para mais
informações: https://kubernetes.io/docs/concepts/services-networking/network-policies/.
As Network Policies permitem que os usuários definam regras de rede para controlar o tráfego de entrada e saída entre os pods e aplicativos dentro do cluster
Kubernetes, garantindo que os dados sejam transmitidos de forma eficiente usando o kubectl. As Network Policies são definidas usando um arquivo YAML, onde os
usuários podem especificar as regras de rede para controlar o tráfego de entrada e saída entre os pods e aplicativos dentro do cluster Kubernetes, garantindo
que os dados sejam transmitidos de forma eficiente usando okubectl. Abaixo um exemplo de configuração de Network Policy em um arquivo YAML para uma Network
Policy do Kubernetes:

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: allow-internet-only
spec:
  podSelector: { }
  policyTypes:
    - Egress
  egress:
    - to:
        - ipBlock:
            cidr: 0.0.0.0/0
            except:
              - 10.0.0.0/8
              - 192.168.0.0/16
              - 172.16.0.0/20
---
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: allow-dns
spec:
  podSelector: { }
  policyTypes:
    - Egress
  egress:
    - to:
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: kube-system
          podSelector:
            matchLabels:
              k8s-app: kube-dns
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: frontend
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: frontend
  policyTypes:
    - Egress
    - Ingress
  ingress:
    - from:
        - ipBlock:
            cidr: 0.0.0.0/0
  egress:
    - to:
        - podSelector:
            matchLabels:
              app: backend
      ports:
        - protocol: TCP
          port: 80
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: backend
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: backend
  policyTypes:
    - Egress
    - Ingress
  egress:
    - to:
        - podSelector:
            matchLabels:
              app: database
      ports:
        - protocol: TCP
          port: 80
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: frontend
      ports:
        - protocol: TCP
          port: 80
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: database
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: database
  policyTypes:
    - Ingress
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: backend
      ports:
        - protocol: TCP
          port: 80
```