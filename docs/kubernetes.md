--Arquitetura de Kubernetes: control plane
Gerenciamento de clusters do Kubernetes é realizado por meio de um conjunto de componentes que formam o plano de
controle (control plane). Esses componentes são responsáveis por manter o estado desejado do cluster, tomar decisões de
agendamento, gerenciar a comunicação entre os nós e garantir a disponibilidade dos serviços. Os principais componentes
do control plane incluem:
api server - (POD) -> é o componente central do control plane, responsável por expor a API do Kubernetes e servir como
ponto de
entrada para todas as operações do cluster. Ele é responsável por autenticar e autorizar solicitações, validar e
processar objetos do Kubernetes, e manter o estado desejado do cluster. Ele também é responsável por
armazenar o estado do cluster no etcd, que é um banco de dados chave-valor distribuído usado para armazenar a
configuração e o estado do cluster.
etcd - (Banco de dados) -> é um banco de dados chave-valor distribuído usado para armazenar a configuração e o estado do
cluster. Ele é
projetado para ser altamente disponível e consistente, garantindo que o estado do cluster seja sempre preciso e
atualizado. O etcd é implementado em Go e é usado pelo API server para armazenar o estado desejado do cluster, bem como
para armazenar informações sobre os nós, pods, serviços e outros recursos do Kubernetes.
cloud controller - (POD) -> responsável por interagir com provedores de nuvem para gerenciar recursos de infraestrutura,
como
balanceadores de carga, volumes de armazenamento e instâncias de máquinas virtuais. Ele é projetado para ser modular,
permitindo que o Kubernetes suporte uma variedade de provedores de nuvem, como AWS, Azure e Google Cloud.
controller manager - (POD) -> é responsável por executar os controladores que gerenciam o estado do cluster. Ele inclui
controladores para gerenciar nós, pods, serviços, endpoints e outros recursos do Kubernetes. O controller manager é
projetado para ser altamente disponível, permitindo que o Kubernetes continue a operar mesmo se
um controlador falhar.
scheduler - (POD) -> é responsável por agendar os pods nos nós de trabalho com base em uma série de critérios, como
recursos
disponíveis, afinidade e anti-afinidade, e políticas de tolerância. Projetado para
ser altamente eficiente, permitindo que o Kubernetes agende rapidamente os pods em clusters de grande escala.

--Arquitetura de Kubernetes: data plane
O data plane do Kubernetes é composto pelos nós de trabalho (worker nodes) que executam as cargas de trabalho (pods) e
são gerenciados pelo control plane. Cada nó de trabalho possui um agente chamado kubelet, que é responsável por garantir
que os contêineres estejam em execução e saudáveis. O data plane também inclui o kube-proxy, que é responsável por
gerenciar a rede e o balanceamento de carga entre os pods. Os principais componentes do data plane incluem:
worker nodes -> são os nós de trabalho que executam as cargas de trabalho (pods) e são gerenciados pelo control plane.
Cada nó de trabalho é responsável por executar os pods agendados pelo scheduler e garantir que eles estejam em execução
e saudáveis. Os nós de trabalho podem ser máquinas físicas ou virtuais e são projetados para ser altamente escaláveis,
permitindo que o Kubernetes gerencie clusters de grande escala com milhares de nós.
kubelet -> é o agente que roda em cada nó de trabalho e é responsável por garantir que os contêineres estejam em
execução e saudáveis. Ele se comunica com o API server para receber instruções sobre quais pods devem ser executados no
nó e para relatar o status dos pods em execução. Garantindo que os pods sejam mantidos em execução mesmo em caso de
falhas temporárias.
kube-proxy -> é responsável por gerenciar a rede e o balanceamento de carga entre os pods. Ele implementa as
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
kind create cluster -> cria um cluster Kubernetes local usando contêineres Docker.
kind create cluster --name <nome-do-cluster> -> cria um cluster Kubernetes local com um nome específico usando
contêineres Docker.
kind create cluster --config <caminho-para-configuração> -> cria um cluster Kubernetes local usando um arquivo de
configuração personalizado.
kind create cluster --image <imagem-do-node> -> cria um cluster Kubernetes local usando uma imagem personalizada para os
nós.
kind create cluster --wait -> cria um cluster Kubernetes local e aguarda até que o cluster esteja pronto antes de
retornar.
kind create cluster --kubeconfig <caminho-para-kubeconfig> -> cria um cluster Kubernetes local e salva o arquivo
kubeconfig em um caminho específico.
kind create cluster --retain -> cria um cluster Kubernetes local e mantém os contêineres Docker mesmo após a exclusão do
cluster.
kind create cluster --nodes <número-de-nós> -> cria um cluster Kubernetes local com um número específico de nós.
kind create cluster --control-plane <número-de-nós-de-control-plane> -> cria um cluster Kubernetes local com um número
específico de nós de control plane.
kind delete cluster -> exclui um cluster Kubernetes local criado com o Kind.
kind get clusters -> lista os clusters Kubernetes locais criados com o Kind.
kind get nodes -> lista os nós de trabalho (worker nodes) em um cluster Kubernetes local criado com o Kind.
kind get pods -> lista os pods em um cluster Kubernetes local criado com o Kind.
kind get services -> lista os serviços em um cluster Kubernetes local criado com o Kind.
kind get deployments -> lista os deployments em um cluster Kubernetes local criado com o Kind.
kind get replicasets -> lista os ReplicaSets em um cluster Kubernetes local criado com o Kind.
kind get statefulsets -> lista os StatefulSets em um cluster Kubernetes local criado com o Kind.
kind get daemonsets -> lista os DaemonSets em um cluster Kubernetes local criado com o Kind.
kind get ingress -> lista os Ingresses em um cluster Kubernetes local criado com o Kind.
kind get configmaps -> lista os ConfigMaps em um cluster Kubernetes local criado com o Kind.
kind get secrets -> lista os Secrets em um cluster Kubernetes local criado com o Kind.
kind get namespaces -> lista os namespaces em um cluster Kubernetes local criado com o Kind.
kind get events -> lista os eventos em um cluster Kubernetes local criado com o Kind.

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
kubectl get -> lista os recursos do Kubernetes, como pods, serviços, deployments e outros objetos.
kubectl describe -> exibe detalhes sobre um recurso específico do Kubernetes, como um pod ou serviço.
kubectl create -> cria um recurso do Kubernetes a partir de um arquivo de configuração ou diretamente na linha de
comando.
kubectl apply -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de configuração, criando ou
atualizando o recurso conforme necessário.
kubectl delete -> exclui um recurso do Kubernetes, como um pod, serviço ou deployment.
kubectl logs -> exibe os logs de um pod específico, permitindo que os usuários monitorem o comportamento dos contêineres
em execução.
kubectl exec -> executa um comando em um contêiner em execução dentro de um pod, permitindo que os usuários interajam
diretamente com os contêineres para depuração ou administração.
kubectl port-forward -> encaminha uma porta local para um pod específico, permitindo que os usuários acessem serviços em
execução dentro do cluster Kubernetes a partir de suas máquinas locais.
kubectl scale -> escala um recurso do Kubernetes, como um deployment ou replicaset, aumentando ou diminuindo o número de
réplicas conforme necessário.
kubectl rollout -> gerencia o processo de implantação de um recurso do Kubernetes, permitindo que os usuários monitorem
o status da implantação, pausem ou retomem a implantação, e revertam para uma versão anterior se necessário.
kubectl top -> exibe o uso de recursos, como CPU e memória, para pods ou nós em um cluster Kubernetes, permitindo que os
usuários monitorem o desempenho e a utilização dos recursos em seus clusters Kubernetes.
kubectl config -> gerencia os arquivos de configuração do Kubernetes, permitindo que os usuários configurem e alternem
entre diferentes clusters Kubernetes, usuários e contextos.
kubectl apply -f <arquivo.yaml> -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo de
configuração YAML, criando ou atualizando o recurso conforme necessário.
kubectl get pods -> lista os pods em um cluster Kubernetes, mostrando informações como nome, status, idade e outros
detalhes relevantes.
kubectl describe pod <nome-do-pod> -> exibe detalhes sobre um pod específico, incluindo informações sobre os contêineres
em execução, eventos relacionados e outros detalhes importantes para a depuração e administração do pod.
kubectl logs <nome-do-pod> -> exibe os logs de um pod específico, permitindo que os usuários monitorem o comportamento
dos contêineres em execução e identifiquem possíveis problemas ou erros.
kubectl exec -it <nome-do-pod> -- <comando> -> executa um comando interativo em um contêiner em execução dentro de um
pod, permitindo que os usuários interajam diretamente com os contêineres para depuração ou administração.
kubectl port-forward <nome-do-pod> <porta-local>:<porta-do-pod> -> encaminha uma porta local para um pod específico,
permitindo que os usuários acessem serviços em execução dentro do cluster Kubernetes a partir de suas máquinas locais.
kubectl scale deployment <nome-do-deployment> --replicas=<número-de-réplicas> -> escala um deployment específico,
aumentando ou diminuindo o número de réplicas conforme necessário para atender à demanda ou otimizar o uso de recursos.
kubectl rollout status deployment <nome-do-deployment> -> monitora o status da implantação de um deployment específico,
permitindo que os usuários verifiquem se a implantação foi bem-sucedida, se há falhas ou se a implantação está em
andamento.
kubectl config use-context <nome-do-contexto> -> alterna para um contexto específico em um arquivo de configuração do
Kubernetes, permitindo que os usuários gerenciem e operem diferentes clusters Kubernetes, usuários e contextos de forma
eficiente.    
kubectl config view -> exibe o conteúdo do arquivo de configuração do Kubernetes, mostrando informações sobre os
clusters, usuários e contextos configurados, permitindo que os usuários verifiquem e gerenciem suas configurações de
acesso ao Kubernetes.
kubectl config get-contexts -> lista os contextos disponíveis em um arquivo de configuração do Kubernetes, mostrando
informações sobre os clusters, usuários e contextos configurados, permitindo que os usuários escolham o contexto
apropriado para suas operações no Kubernetes.
kubectl config current-context -> exibe o contexto atual em uso em um arquivo de configuração do Kubernetes, permitindo
que os usuários verifiquem qual cluster, usuário e contexto estão ativos para suas operações no Kubernetes.
kubectl apply -f <arquivo.yaml> -> aplica as alterações a um recurso do Kubernetes a partir de um arquivo deconfiguração
YAML, criando ou atualizando o recurso conforme necessário. Este comando é amplamente utilizado paragerenciar recursos
do Kubernetes de forma declarativa, permitindo que os usuários definam o estado desejado dos recursos em arquivos de
configuração e apliquem essas configurações ao cluster Kubernetes de maneira eficiente e consistente.
kubectl api-resources -> lista os tipos de recursos disponíveis na API do Kubernetes, mostrando informações sobre os recursos
suportados, suas versões e se eles são recursos de namespace ou de cluster, permitindo que os usuários entendam os recursos disponíveis para gerenciamento e
operação em seus clusters Kubernetes.
kubectl get pod -n kube-system <pod-name> -> exibe detalhes sobre um pod específico no namespace kube-system, que é o namespace onde os componentes do control
plane do Kubernetes geralmente são executados. Este comando é útil para verificar o status e os logs dos pods do control plane, permitindo que os usuários
monitorem a saúde e o desempenho dos componentes essenciais do Kubernetes em seus clusters.
kubectl get pod -n kube-system <pod-name> -o -> exibe detalhes sobre um pod específico no namespace kube-system em um formato de saída específico, como JSON ou
YAML, permitindo que os usuários obtenham informações detalhadas sobre o pod e seus recursos associados para depuração e administração avançada no Kubernetes.
kubectl get pod -n kube-system <pod-name> -o json -> exibe detalhes sobre um pod específico no namespace kube-system em formato JSON, permitindo que os usuários
obtenham informações estruturadas e detalhadas sobre o pod e seus recursos associados para depuração e administração avançada no Kubernetes.
kubectl get pod -n kube-system <pod-name> -o yaml -> exibe detalhes sobre um pod específico no namespace kube-system em formato YAML, permitindo que os usuários
obtenham informações estruturadas e detalhadas sobre o pod e seus recursos associados para depuração e administração avançada no Kubernetes.
kubectl get pod -n kube-system <pod-name> -o wide -> exibe detalhes sobre um pod específico no namespace kube-system em um formato de saída mais amplo,
mostrando informações adicionais como o nó onde o pod está em execução, o endereço IP do pod e outras informações relevantes para monitoramento e administração
no Kubernetes.
kubectl get pod -n kube-system <pod-name> -o =jsonpath='{.status.phase}' -> exibe o status de um pod específico no namespace kube-system usando uma expressão
jsonpath para extrair apenas o valor do campo status.phase, permitindo que os usuários obtenham informações específicas sobre o estado do pod de forma eficiente
no Kubernetes.
kubectl get pod -Aowide -> lista todos os pods em todos os namespaces com informações adicionais, mostrando detalhes como o namespace, o nome do pod, o status,
a idade, o nó onde o pod está em execução e outras informações relevantes para monitoramento e administração em um cluster Kubernetes.
kubectl get pod -n kube-system --show-labels -> lista os pods no namespace kube-system e exibe as labels associadas a cada pod, permitindo que os usuários vejam
as labels usadas para organizar e selecionar os pods no Kubernetes, o que é útil para gerenciamento e administração eficiente dos recursos do cluster.
kubectl get pod -n kube-system --show-labels <label-selector> -> lista os pods no namespace kube-system que correspondem a um seletor de labels específico,
permitindo que os usuários filtrem os pods com base em suas labels para gerenciamento e administração eficiente dos recursos do cluster Kubernetes.
kubectl get -n kube-system etcd-comunidade-devops-control-plane -oyaml -> exibe detalhes sobre o pod etcd-comunidade-devops-control-plane no namespace
kube-system em formato YAML, permitindo que os usuários obtenham informações estruturadas e detalhadas sobre o pod etcd e seus recursos associados para
depuração e administração avançada no Kubernetes.

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
etcdctl get / --prefix -> lista todas as chaves e valores armazenados no banco de dados etcd, mostrando informações sobre a configuração e o estado do cluster
Kubernetes.
etcdctl put <chave> <valor> -> adiciona ou atualiza uma chave e valor no banco de dados etcd, permitindo que os usuários gerenciem a configuração e o estado do
cluster Kubernetes de forma eficiente usando o etcdctl.
etcdctl del <chave> -> exclui uma chave do banco de dados etcd, permitindo que os usuários removam informações desnecessárias ou obsoletas do cluster Kubernetes
usando o etcdctl.
etcdctl member list -> lista os membros do cluster etcd, mostrando informações sobre os nós do cluster etcd, suas IDs, status e outras informações relevantes
para monitoramento e administração do cluster etcd usando o etcdctl.
etcdctl member add <nome-do-membro> --peer-urls=<url-do-peer> -> adiciona um novo membro ao cluster etcd, permitindo que os usuários expandam o cluster etcd
adicionando novos nós usando o etcdctl.
etcdctl member remove <id-do-membro> -> remove um membro do cluster etcd, permitindo que os usuários reduzam o cluster etcd removendo nós usando o etcdctl.
etcdctl snapshot save <caminho-do-arquivo> -> salva um snapshot do banco de dados etcd em um arquivo, permitindo que os usuários criem backups do estado do
cluster Kubernetes usando o etcdctl.
etcdctl snapshot restore <caminho-do-arquivo> -> restaura um snapshot do banco de dados etcd a partir de um arquivo, permitindo que os usuários recuperem o
estado do cluster Kubernetes a partir de um backup usando o etcdctl.
etcdctl endpoint health -> verifica a saúde dos endpoints do cluster etcd, mostrando informações sobre o status dos nós do cluster etcd e permitindo que os
usuários monitorem a saúde do cluster etcd usando o etcdctl.
etcdctl endpoint status -> exibe o status dos endpoints do cluster etcd, mostrando informações detalhadas sobre os nós do cluster etcd, como a versão do etcd, o
número de membros, o tempo de resposta e outras informações relevantes para monitoramento e administração do cluster etcd usando o etcdctl.
etcdctl endpoint status --write-out=table -> exibe o status dos endpoints do cluster etcd em formato de tabela, mostrando informações detalhadas sobre os nós do
cluster etcd de forma organizada e fácil de ler para monitoramento e administração do cluster etcd usando o etcdctl.
etcdctl endpoint status --write-out=fields -> exibe o status dos endpoints do cluster etcd em formato de campos, mostrando informações detalhadas sobre os nós
do cluster etcd em um formato mais compacto e fácil de processar para monitoramento e administração do cluster etcd usando o etcdctl.
etcdctl endpoint status --write-out=json -> exibe o status dos endpoints do cluster etcd em formato JSON, mostrando informações detalhadas sobre os nós do
cluster etcd em um formato estruturado e fácil de processar para monitoramento e administração do cluster etcd usando o etcdctl.
etcdctl endpoint status --write-out=yaml -> exibe o status dos endpoints do cluster etcd em formato YAML, mostrando informações detalhadas sobre os nós do
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
apiVersion: apps/v1
kind: Deployment
metadata:
  name: meu-deployment
  labels:
    app: minha-aplicacao
spec:
  replicas: 3
  selector:
    matchLabels:
      app: minha-aplicacao
  template:
    metadata:
      labels:
        app: minha-aplicacao
    spec:
      containers:
        - name: meu-container
          image: minha-imagem:latest
          ports:
            - containerPort: 80
```