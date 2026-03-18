# ☸️ Kubernetes — Guia de Referência

## 📋 Sumário

- [Arquitetura: Control Plane](#arquitetura-control-plane)
- [Arquitetura: Data Plane](#arquitetura-data-plane)
- [Kind](#kind)
    - [Comandos Kind](#comandos-kind)
    - [Exemplo de configuração Kind](#exemplo-de-configuração-kind)
- [Kubectl](#kubectl)
    - [Comandos Kubectl](#comandos-kubectl)
    - [Configurando o Kubectl para o Kind](#configurando-o-kubectl-para-o-kind)
    - [Merge do Kubeconfig](#merge-do-kubeconfig)
- [etcd](#etcd)
    - [Configurando o etcdctl](#configurando-o-etcdctl)
    - [Backup e Snapshot do etcd](#backup-e-snapshot-do-etcd)
    - [Comandos etcdctl](#comandos-etcdctl)
- [YAML no Kubernetes](#yaml-no-kubernetes)
- [Namespaces](#namespaces)
    - [Namespaces Padrão](#namespaces-padrão)
    - [Comandos de Namespace](#comandos-de-namespace)
- [Pods](#pods)
    - [Comandos de Pods](#comandos-de-pods)
    - [Init Containers](#init-containers)
    - [Multi-container Pods](#multi-container-pods)
    - [Static Pods](#static-pods)
    - [Lifecycle dos Pods](#lifecycle-dos-pods)

---

## Arquitetura: Control Plane

O gerenciamento de clusters do Kubernetes é realizado por um conjunto de componentes que formam o **plano de controle (control plane)**. Esses componentes são
responsáveis por manter o estado desejado do cluster, tomar decisões de agendamento, gerenciar a comunicação entre os nós e garantir a disponibilidade dos
serviços.

| Componente             | Tipo           | Descrição                                                                                                                                    |
|------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| **API Server**         | POD            | Componente central do control plane. Expõe a API do Kubernetes, autentica/autoriza solicitações, valida objetos e armazena o estado no etcd. |
| **etcd**               | Banco de dados | Banco de dados chave-valor distribuído, altamente disponível e consistente. Armazena toda a configuração e estado do cluster.                |
| **Cloud Controller**   | POD            | Interage com provedores de nuvem (AWS, Azure, GCP) para gerenciar recursos como balanceadores de carga, volumes e VMs.                       |
| **Controller Manager** | POD            | Executa controladores que gerenciam o estado do cluster (nós, pods, serviços, endpoints etc.). Projetado para alta disponibilidade.          |
| **Scheduler**          | POD            | Agenda pods nos nós de trabalho com base em recursos disponíveis, afinidade, anti-afinidade e políticas de tolerância.                       |

---

## Arquitetura: Data Plane

O **data plane** é composto pelos nós de trabalho (worker nodes) que executam as cargas de trabalho (pods), gerenciados pelo control plane.

| Componente       | Descrição                                                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **Worker Nodes** | Executam os pods agendados pelo scheduler. Podem ser máquinas físicas ou virtuais, projetadas para alta escalabilidade.     |
| **kubelet**      | Agente em cada nó. Comunica-se com o API Server, garante que os contêineres estejam em execução e relata o status dos pods. |
| **kube-proxy**   | Gerencia a rede e o balanceamento de carga entre os pods, implementando regras de rede para comunicação interna e externa.  |

---

## Kind

O **Kind** (Kubernetes IN Docker) é uma ferramenta de código aberto que permite criar clusters Kubernetes locais usando contêineres Docker. É ideal para
desenvolvimento, testes de integração e aprendizado, sem necessidade de infraestrutura de nuvem.

### Comandos Kind

| Comando                                      | Descrição                                                    |
|----------------------------------------------|--------------------------------------------------------------|
| `kind create cluster`                        | Cria um cluster Kubernetes local.                            |
| `kind create cluster --name <nome>`          | Cria um cluster com nome específico.                         |
| `kind create cluster --config <arquivo>`     | Cria um cluster com configuração personalizada.              |
| `kind create cluster --image <imagem>`       | Cria um cluster usando uma imagem customizada para os nós.   |
| `kind create cluster --wait`                 | Aguarda o cluster ficar pronto antes de retornar.            |
| `kind create cluster --kubeconfig <caminho>` | Salva o kubeconfig em um caminho específico.                 |
| `kind create cluster --retain`               | Mantém os contêineres Docker mesmo após exclusão do cluster. |
| `kind delete cluster`                        | Exclui o cluster local.                                      |
| `kind delete cluster --name <nome>`          | Exclui um cluster com nome específico.                       |
| `kind get clusters`                          | Lista os clusters locais criados com o Kind.                 |
| `kind get nodes`                             | Lista os nós do cluster.                                     |
| `kind export kubeconfig --name <nome>`       | Exporta o kubeconfig do cluster (útil no Windows).           |

### Exemplo de configuração Kind

Criando o cluster com arquivo de configuração:

```bash
kind create cluster --config config.yaml --name comunidade-devops --kubeconfig config
```

### Exemplo de arquivo de configuração Kind

Cluster com 1 control plane e 2 workers, com mapeamento de portas:

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

---

## Kubectl

O **kubectl** é a ferramenta de linha de comando oficial para interagir com clusters Kubernetes. Permite gerenciar pods, serviços, deployments e outros recursos
via comandos simples. É amplamente utilizado por desenvolvedores, administradores e engenheiros de DevOps.

### Comandos Kubectl

#### Operações Gerais

| Comando                             | Descrição                                            |
|-------------------------------------|------------------------------------------------------|
| `kubectl get <recurso>`             | Lista recursos (pods, services, deployments etc.).   |
| `kubectl describe <recurso> <nome>` | Exibe detalhes de um recurso específico.             |
| `kubectl create -f <arquivo.yaml>`  | Cria um recurso a partir de um arquivo YAML.         |
| `kubectl apply -f <arquivo.yaml>`   | Aplica configurações (cria ou atualiza o recurso).   |
| `kubectl delete <recurso> <nome>`   | Exclui um recurso.                                   |
| `kubectl api-resources`             | Lista todos os tipos de recursos disponíveis na API. |

#### Pods

| Comando                                         | Descrição                                   |
|-------------------------------------------------|---------------------------------------------|
| `kubectl get pods`                              | Lista todos os pods no namespace atual.     |
| `kubectl get pods -A`                           | Lista todos os pods em todos os namespaces. |
| `kubectl get pods -w`                           | Monitora os pods em tempo real.             |
| `kubectl get pods -n <namespace>`               | Lista pods em um namespace específico.      |
| `kubectl get pods -o wide`                      | Exibe informações adicionais (nó, IP etc.). |
| `kubectl get pods -o yaml`                      | Exibe a definição completa em YAML.         |
| `kubectl get pods -o json`                      | Exibe a definição completa em JSON.         |
| `kubectl get pods --show-labels`                | Exibe as labels de cada pod.                |
| `kubectl describe pod <nome>`                   | Detalha um pod específico.                  |
| `kubectl logs <nome-do-pod>`                    | Exibe os logs de um pod.                    |
| `kubectl logs <nome-do-pod> -f`                 | Acompanha os logs em tempo real.            |
| `kubectl exec -it <nome-do-pod> -- <cmd>`       | Executa um comando interativo no contêiner. |
| `kubectl port-forward <pod> <local>:<pod-port>` | Encaminha porta local para o pod.           |
| `kubectl delete pod <nome>`                     | Exclui um pod.                              |
| `kubectl delete pod <nome> -n <namespace>`      | Exclui um pod em um namespace específico.   |

#### Deployments

| Comando                                          | Descrição                        |
|--------------------------------------------------|----------------------------------|
| `kubectl get deployments`                        | Lista os deployments.            |
| `kubectl scale deployment <nome> --replicas=<n>` | Escala o número de réplicas.     |
| `kubectl rollout status deployment <nome>`       | Verifica o status de um rollout. |
| `kubectl rollout undo deployment <nome>`         | Reverte para a versão anterior.  |
| `kubectl delete deployment <nome>`               | Exclui um deployment.            |

#### Serviços

| Comando                         | Descrição          |
|---------------------------------|--------------------|
| `kubectl get services`          | Lista os serviços. |
| `kubectl delete service <nome>` | Exclui um serviço. |

#### Monitoramento

| Comando             | Descrição                            |
|---------------------|--------------------------------------|
| `kubectl top pods`  | Exibe uso de CPU e memória dos pods. |
| `kubectl top nodes` | Exibe uso de CPU e memória dos nós.  |

#### Contextos e Configuração

| Comando                                                 | Descrição                                    |
|---------------------------------------------------------|----------------------------------------------|
| `kubectl config view`                                   | Exibe o conteúdo do kubeconfig.              |
| `kubectl config view --minify`                          | Exibe apenas o contexto atual.               |
| `kubectl config get-contexts`                           | Lista os contextos disponíveis.              |
| `kubectl config current-context`                        | Exibe o contexto ativo.                      |
| `kubectl config use-context <nome>`                     | Alterna para um contexto específico.         |
| `kubectl config set-context --current --namespace=<ns>` | Define o namespace padrão do contexto atual. |

#### Formatos de saída avançados

```bash
# Filtrar campo específico com jsonpath
kubectl get pod <nome> -n kube-system -o jsonpath='{.status.phase}'

# Listar todos os pods com informações detalhadas
kubectl get pod -A -o wide

# Exibir pod com labels no namespace kube-system
kubectl get pod -n kube-system --show-labels

# Exibir um pod do etcd em YAML
kubectl get -n kube-system etcd-comunidade-devops-control-plane -o yaml
```

### Configurando o Kubectl para o Kind

#### ✅ Opção 1 — Exportar manualmente o admin.config

1. Crie o cluster com o Kind:
   ```bash
   kind create cluster --config config.yaml --name comunidade-devops --kubeconfig config
   ```
2. Acesse o contêiner do control plane:
   ```bash
   docker exec -it <nome-do-contêiner> bash
   ```
3. Copie o conteúdo de `/etc/kubernetes/admin.config`.
4. No Windows, cole o conteúdo em `C:\Users\SeuUsuario\.kube\config`.
5. Se ocorrer o erro `dial tcp: lookup comunidade-devops-control-plane: no such host`, reexporte o kubeconfig:
   ```bash
   kind export kubeconfig --name comunidade-devops
   ```
   Verifique se o endereço foi corrigido para `https://127.0.0.1:PORTA`:
   ```bash
   kubectl config view --minify
   ```

> ⚠️ **No Windows**, o kubectl roda fora do WSL/Docker e não enxerga a rede interna dos contêineres Kind. Use sempre `kind export kubeconfig` para corrigir o
> hostname.

#### ✅ Opção 2 — Usar o contexto gerado automaticamente

1. Crie o cluster:
   ```bash
   kind create cluster --name <nome-do-cluster>
   ```
2. O Kind configura automaticamente o kubeconfig. Alterne para o contexto:
   ```bash
   kubectl config use-context kind-<nome-do-cluster>
   ```
3. Verifique o contexto ativo:
   ```bash
   kubectl config current-context
   ```
4. Teste o acesso ao cluster:
   ```bash
   kubectl get pods -A
   ```

### Merge do Kubeconfig

Para combinar múltiplos arquivos kubeconfig em um único arquivo:

```bash
kubectl config view --merge --flatten > merged-kubeconfig.yaml
```

Ative o arquivo combinado:

```bash
# Linux/macOS
export KUBECONFIG=merged-kubeconfig.yaml

# Windows (CMD)
set KUBECONFIG=merged-kubeconfig.yaml

# Windows (PowerShell)
$env:KUBECONFIG = "merged-kubeconfig.yaml"
```

> ⚠️ **Atenção:** Os nomes de `cluster`, `user` e `context` devem ser **únicos** no arquivo combinado. Em caso de conflito, edite manualmente o arquivo para
> renomear as entradas duplicadas.

Gerencie os contextos disponíveis:

```bash
kubectl config get-contexts
kubectl config use-context <nome-do-contexto>
```

---

## etcd

O **etcd** é um banco de dados chave-valor distribuído usado pelo Kubernetes para armazenar toda a configuração e o estado do cluster.

### Configurando o etcdctl

O **etcdctl** é a CLI oficial para interagir com o etcd.

1. Acesse o contêiner do control plane:
   ```bash
   docker exec -it <nome-do-contêiner> bash
   ```
2. Os certificados estão em `/etc/kubernetes/pki/etcd/`.
3. Exporte as variáveis de ambiente:
   ```bash
   export ETCDCTL_API=3
   export ETCDCTL_CACERT=/etc/kubernetes/pki/etcd/ca.crt
   export ETCDCTL_CERT=/etc/kubernetes/pki/etcd/server.crt
   export ETCDCTL_KEY=/etc/kubernetes/pki/etcd/server.key
   ```
4. Para reutilizar, salve as variáveis em um arquivo:
   ```bash
   cat <<EOF > etcdctl.env
   export ETCDCTL_API=3
   export ETCDCTL_CACERT=/etc/kubernetes/pki/etcd/ca.crt
   export ETCDCTL_CERT=/etc/kubernetes/pki/etcd/server.crt
   export ETCDCTL_KEY=/etc/kubernetes/pki/etcd/server.key
   EOF

   source etcdctl.env
   ```

### Backup e Snapshot do etcd

> ⚠️ O etcd contém informações sensíveis. Faça backups regulares e sempre teste a restauração em ambiente de teste antes de aplicar em produção.

**Criar snapshot:**

```bash
etcdctl snapshot save /var/lib/etcd/snapshot.db
```

**Restaurar snapshot:**

```bash
etcdctl snapshot restore /var/lib/etcd/snapshot.db
```

### Comandos etcdctl

| Comando                                       | Descrição                                          |
|-----------------------------------------------|----------------------------------------------------|
| `etcdctl get / --prefix`                      | Lista todas as chaves e valores armazenados.       |
| `etcdctl put <chave> <valor>`                 | Adiciona ou atualiza uma chave-valor.              |
| `etcdctl del <chave>`                         | Exclui uma chave.                                  |
| `etcdctl member list`                         | Lista os membros do cluster etcd.                  |
| `etcdctl member add <nome> --peer-urls=<url>` | Adiciona um novo membro ao cluster.                |
| `etcdctl member remove <id>`                  | Remove um membro do cluster.                       |
| `etcdctl snapshot save <caminho>`             | Salva um snapshot do banco de dados.               |
| `etcdctl snapshot restore <caminho>`          | Restaura o banco de dados a partir de um snapshot. |
| `etcdctl endpoint health`                     | Verifica a saúde dos endpoints.                    |
| `etcdctl endpoint status`                     | Exibe o status dos endpoints.                      |
| `etcdctl endpoint status --write-out=table`   | Status em formato de tabela.                       |
| `etcdctl endpoint status --write-out=json`    | Status em formato JSON.                            |
| `etcdctl endpoint status --write-out=yaml`    | Status em formato YAML.                            |

---

## YAML no Kubernetes

O Kubernetes usa arquivos **YAML** para definir e gerenciar recursos de forma **declarativa**. Os arquivos seguem uma estrutura padrão com os campos:

| Campo        | Descrição                                             |
|--------------|-------------------------------------------------------|
| `apiVersion` | Versão da API do Kubernetes (ex: `v1`, `apps/v1`).    |
| `kind`       | Tipo do recurso (ex: `Pod`, `Deployment`, `Service`). |
| `metadata`   | Metadados do recurso (nome, namespace, labels etc.).  |
| `spec`       | Especificação do estado desejado do recurso.          |

### Exemplo: Pod simples com Nginx

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

### Validar YAML antes de aplicar

```bash
kubectl apply --dry-run=client -f <arquivo.yaml>
```

---

## Namespaces

Um **namespace** é uma forma de organizar e isolar recursos dentro de um cluster Kubernetes. Permite criar múltiplos ambientes lógicos (desenvolvimento, teste,
produção) dentro do mesmo cluster, evitando conflitos de nomes e possibilitando controle de acesso por ambiente.

### Namespaces Padrão

| Namespace            | Descrição                                                                      |
|----------------------|--------------------------------------------------------------------------------|
| `default`            | Namespace padrão para recursos criados sem namespace explícito.                |
| `kube-system`        | Componentes do control plane (API server, scheduler, controller manager etc.). |
| `kube-public`        | Recursos acessíveis publicamente por qualquer usuário do cluster.              |
| `kube-node-lease`    | Informações de lease dos nós, usadas para monitorar a saúde dos nós.           |
| `local-path-storage` | Recursos do provisionador de armazenamento local para pods.                    |

### Comandos de Namespace

| Comando                                                 | Descrição                                     |
|---------------------------------------------------------|-----------------------------------------------|
| `kubectl create namespace <nome>`                       | Cria um novo namespace.                       |
| `kubectl get namespaces`                                | Lista todos os namespaces.                    |
| `kubectl delete namespace <nome>`                       | Exclui um namespace e todos os seus recursos. |
| `kubectl get pods -n <namespace>`                       | Lista pods em um namespace específico.        |
| `kubectl apply -f <arquivo.yaml> -n <namespace>`        | Aplica um recurso em um namespace específico. |
| `kubectl config set-context --current --namespace=<ns>` | Define o namespace padrão do contexto atual.  |

---

## Pods

Um **pod** é a menor unidade de implantação e execução no Kubernetes. Representa um grupo de um ou mais contêineres que compartilham rede, armazenamento e
recursos de computação. Os pods são **efêmeros** e gerenciados por controladores (Deployments, StatefulSets, DaemonSets).

> 💡 Normalmente cada pod contém um único contêiner, mas é possível ter múltiplos contêineres (padrão **sidecar**) para tarefas auxiliares como monitoramento,
> logging ou proxy reverso.

### Comandos de Pods

| Comando                                                                   | Descrição                                                       |
|---------------------------------------------------------------------------|-----------------------------------------------------------------|
| `kubectl run <nome> --image=<imagem>`                                     | Cria um pod com a imagem especificada.                          |
| `kubectl run <nome> --image=<imagem> --rm -it -- sh`                      | Cria pod temporário com terminal interativo (removido ao sair). |
| `kubectl run <nome> --image=<imagem> --dry-run=client -o yaml`            | Gera o YAML do pod sem criá-lo.                                 |
| `kubectl run <nome> --image=<imagem> --dry-run=client -o yaml > pod.yaml` | Salva o YAML gerado em arquivo.                                 |
| `kubectl apply -f <arquivo.yaml>`                                         | Cria ou atualiza recursos a partir de um YAML.                  |
| `kubectl get pods`                                                        | Lista os pods.                                                  |
| `kubectl get pods -w`                                                     | Monitora pods em tempo real.                                    |
| `kubectl describe pod <nome>`                                             | Exibe detalhes completos de um pod.                             |
| `kubectl logs <nome>`                                                     | Exibe os logs do pod.                                           |
| `kubectl exec -it <nome> -- sh`                                           | Abre terminal interativo no contêiner.                          |
| `kubectl port-forward <nome> <local>:<pod>`                               | Encaminha porta local para o pod.                               |
| `kubectl delete pod <nome>`                                               | Exclui um pod.                                                  |
| `kubectl delete pod <nome> -n <namespace>`                                | Exclui um pod em um namespace específico.                       |

### Manter pod em execução para debug

```yaml
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

---

### Init Containers

Os **init containers** são executados antes dos contêineres principais do pod. São usados para tarefas de inicialização como verificação de dependências,
configuração do ambiente etc.

- São executados em **ordem sequencial**.
- Cada init container deve ser **concluir com sucesso** antes do próximo iniciar.
- Os contêineres principais só iniciam após **todos** os init containers finalizarem.

**Exemplo: aguardar o DNS de um serviço antes de iniciar o Nginx:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-cd
  namespace: default
spec:
  initContainers:
    - name: waitfordns
      image: busybox:latest
      command:
        - sh
        - -c
        - |
          until nslookup mymysql.default.svc.cluster.local; do
            echo "waiting for dns..."
            sleep 2
          done
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

---

### Multi-container Pods

Pods com múltiplos contêineres compartilham o mesmo ambiente de execução (rede, armazenamento), permitindo que colaborem de forma eficiente.

**Exemplo: servidor HTTP com contêiner de debug (sidecar):**

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

> ⚠️ Se o `command` do contêiner `debug` for removido, o pod entrará em **CrashLoopBackOff**, pois o Alpine não possui um processo de longa duração por padrão.

---

### Static Pods

**Static pods** são gerenciados diretamente pelo **kubelet** em um nó específico, sem intervenção do control plane. São usados para executar componentes
essenciais do cluster como `kube-apiserver`, `kube-controller-manager` e `kube-scheduler`.

- Definidos em arquivos YAML no diretório `/etc/kubernetes/manifests/`.
- O kubelet monitora o diretório e cria/remove os pods automaticamente.
- **Não são afetados por falhas do control plane**, garantindo resiliência.

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: static-pod-example
  name: static-pod-example
spec:
  containers:
    - image: httpd
      name: httpd
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

---

### Lifecycle dos Pods

#### Fases do Pod

| Fase        | Descrição                                                          |
|-------------|--------------------------------------------------------------------|
| `Pending`   | Pod criado, aguardando ser agendado em um nó.                      |
| `Running`   | Pod atribuído a um nó e com pelo menos um contêiner em execução.   |
| `Succeeded` | Todos os contêineres finalizaram com sucesso (exit code 0).        |
| `Failed`    | Pelo menos um contêiner finalizou com falha.                       |
| `Unknown`   | Estado desconhecido, geralmente por falha de comunicação com o nó. |

Monitore o ciclo de vida dos pods com:

```bash
kubectl get pods -w
kubectl describe pod <nome>
```

#### Lifecycle Hooks

Os **lifecycle hooks** permitem executar ações em momentos específicos do ciclo de vida do pod:

| Hook        | Momento de execução               |
|-------------|-----------------------------------|
| `postStart` | Logo após o contêiner iniciar.    |
| `preStop`   | Antes do contêiner ser encerrado. |

#### terminationGracePeriodSeconds

Define o tempo (em segundos) que o Kubernetes aguarda antes de forçar a exclusão do pod, dando tempo para tarefas de limpeza.

**Exemplo completo com lifecycle hook e grace period:**

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

Neste exemplo:

- O hook `preStop` executa um `curl` antes do encerramento do contêiner.
- O `terminationGracePeriodSeconds: 60` garante até **60 segundos** para que o hook seja executado antes de o Kubernetes forçar o encerramento.

