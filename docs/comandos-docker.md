# 🐳 Guia Docker — Referência Rápida

> Documentação de referência sobre comandos Docker, Dockerfiles e boas práticas.

---

## Sumário

1. [Instruções do Dockerfile](#1-instruções-do-dockerfile)
2. [Escolhendo uma Imagem Docker](#2-escolhendo-uma-imagem-docker)
3. [Comandos Docker](#3-comandos-docker)
4. [Exemplo — Aplicação Node.js](#4-exemplo--aplicação-nodejs)
5. [Criando a Imagem e Rodando o Container](#5-criando-a-imagem-e-rodando-o-container)
6. [Melhorando a Performance da Imagem](#6-melhorando-a-performance-da-imagem)
7. [Gerenciamento de Containers](#7-gerenciamento-de-containers)
8. [Portas](#8-portas)
9. [Volumes](#9-volumes)
10. [Copiando Arquivos](#10-copiando-arquivos)
11. [Redes (Networks)](#11-redes-networks)

---

## 1. Instruções do Dockerfile

| Instrução             | Descrição                                                                                                       |
|-----------------------|-----------------------------------------------------------------------------------------------------------------|
| `FROM <imagem>`       | Especifica a imagem base. Ex: `FROM ubuntu:latest`                                                              |
| `WORKDIR <path>`      | Define o diretório de trabalho dentro do container. Todos os comandos seguintes serão executados a partir dele. |
| `COPY <src> <dest>`   | Copia arquivos/diretórios do host para dentro do container.                                                     |
| `ADD <src> <dest>`    | Similar ao `COPY`, mas também suporta URLs e extração automática de arquivos `.tar`.                            |
| `RUN <comando>`       | Executa um comando durante o **build** da imagem. Ex: `RUN apt-get update`                                      |
| `ENV <chave>=<valor>` | Define uma variável de ambiente. Ex: `ENV PORT=8080`                                                            |
| `EXPOSE <porta>`      | Documenta que o container escuta em uma porta. Ex: `EXPOSE 80` *(não publica a porta no host)*                  |
| `USER <usuário>`      | Define o usuário que executará os comandos dentro do container. Ex: `USER appuser`                              |
| `CMD ["cmd", "arg"]`  | Comando padrão executado ao iniciar o container. Ex: `CMD ["node", "app.js"]`                                   |
| `ENTRYPOINT ["cmd"]`  | Define o executável principal do container. Argumentos passados ao `docker run` são anexados a ele.             |
| `VOLUME <path>`       | Cria um ponto de montagem para persistência de dados.                                                           |

> **Dica:** `CMD` pode ser sobrescrito em tempo de execução; `ENTRYPOINT` define o binário fixo do container.

---

## 2. Escolhendo uma Imagem Docker

1. **Verifique a imagem oficial** — Acesse o [Docker Hub](https://hub.docker.com) e prefira imagens oficiais, mantidas
   pela comunidade ou pelos fornecedores.
2. **Leia a documentação** — Entenda dependências, variáveis de ambiente, portas expostas e versões disponíveis.
3. **Verifique popularidade e avaliações** — Imagens com muitos downloads e boas avaliações tendem a ser mais
   confiáveis.
4. **Verifique a data de atualização** — Prefira imagens atualizadas regularmente para garantir correções de segurança.
5. **Escaneie vulnerabilidades** — Use ferramentas como [Docker Scout](https://docs.docker.com/scout/)
   ou [Snyk](https://snyk.io) antes de ir para produção.
6. **Teste antes de usar em produção** — Valide o comportamento da imagem em ambiente de desenvolvimento.

---

## 3. Comandos Docker

### 3.1 Imagens

| Comando                                       | Descrição                                                        |
|-----------------------------------------------|------------------------------------------------------------------|
| `docker images`                               | Lista as imagens disponíveis localmente.                         |
| `docker images -q <imagem>`                   | Retorna apenas o ID da imagem especificada.                      |
| `docker pull <imagem>`                        | Baixa uma imagem do Docker Hub.                                  |
| `docker build -t <nome> .`                    | Constrói uma imagem a partir do `Dockerfile` no diretório atual. |
| `docker rmi <image_id>`                       | Remove uma imagem (não pode estar em uso).                       |
| `docker image save -o <arquivo>.tar <imagem>` | Salva uma imagem em arquivo `.tar`.                              |
| `docker image load -i <arquivo>.tar`          | Carrega uma imagem a partir de um arquivo `.tar`.                |
| `docker push <imagem>`                        | Envia uma imagem para um repositório remoto (ex: Docker Hub).    |

### 3.2 Containers

| Comando                                        | Descrição                                                                         |
|------------------------------------------------|-----------------------------------------------------------------------------------|
| `docker run -it ubuntu:latest bash`            | Inicia um container interativo Ubuntu com bash.                                   |
| `docker run -d -p <host>:<container> <imagem>` | Inicia um container em background com mapeamento de porta.                        |
| `docker ps`                                    | Lista os containers em execução.                                                  |
| `docker ps -a`                                 | Lista todos os containers, incluindo parados.                                     |
| `docker start <container>`                     | Inicia um container parado.                                                       |
| `docker stop <container>`                      | Para um container em execução.                                                    |
| `docker rm <container>`                        | Remove um container parado.                                                       |
| `docker exec -it <container> bash`             | Abre um terminal interativo dentro do container.                                  |
| `docker inspect <container>`                   | Exibe detalhes completos sobre o container (configuração, estado, rede, volumes). |

### 3.3 Logs

| Comando                                                 | Descrição                                     |
|---------------------------------------------------------|-----------------------------------------------|
| `docker logs <container>`                               | Exibe os logs do container.                   |
| `docker logs -f <container>`                            | Exibe logs em tempo real *(follow)*.          |
| `docker logs --tail 100 <container>`                    | Exibe apenas as últimas 100 linhas.           |
| `docker logs -t <container>`                            | Exibe logs com timestamps.                    |
| `docker logs --since "2024-01-01T00:00:00" <container>` | Exibe logs a partir de uma data/hora.         |
| `docker logs --until "2024-01-31T23:59:59" <container>` | Exibe logs até uma data/hora.                 |
| `docker logs --details <container>`                     | Exibe logs com detalhes adicionais de origem. |

### 3.4 Rede e Limpeza

| Comando                  | Descrição                                                        |
|--------------------------|------------------------------------------------------------------|
| `docker network ls`      | Lista as redes Docker disponíveis.                               |
| `docker volume ls`       | Lista os volumes Docker disponíveis.                             |
| `docker system prune -a` | Remove containers parados, imagens não utilizadas e redes órfãs. |

---

## 4. Exemplo — Aplicação Node.js

### Dockerfile básico

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["node", "src/index.js"]
```

### Verificando a aplicação

1. Certifique-se de que o `Dockerfile` está na raiz do projeto e que os arquivos necessários estão presentes (
   `package.json`, `src/index.js`, etc.).
2. Confirme que a porta exposta no `Dockerfile` coincide com a porta usada pela aplicação.
3. Verifique os logs ou acesse o container interativamente após o build:

```bash
docker build -t minha-aplicacao .
docker run -it minha-aplicacao
```

---

## 5. Criando a Imagem e Rodando o Container

**Build da imagem:**

```bash
docker build -t minha-aplicacao .
```

**Rodar o container em background com mapeamento de porta:**

```bash
docker run -dp 3000:3000 minha-aplicacao
```

Acesse a aplicação em: [http://localhost:3000](http://localhost:3000)

---

## 6. Melhorando a Performance da Imagem

| Prática                          | Descrição                                                                             |
|----------------------------------|---------------------------------------------------------------------------------------|
| **Use imagens base leves**       | Prefira variantes `alpine` ou `slim` para reduzir o tamanho final.                    |
| **Minimize camadas**             | Combine comandos `RUN` com `&&` para reduzir o número de camadas.                     |
| **Use `.dockerignore`**          | Exclua `node_modules`, logs e arquivos locais desnecessários do build.                |
| **Otimize dependências**         | Instale apenas o que é necessário para produção.                                      |
| **Aproveite o cache**            | Copie `package.json` e instale dependências **antes** de copiar o restante do código. |
| **Limpe arquivos temporários**   | Remova caches de pacotes após instalações (`rm -rf /var/cache/apk/*`).                |
| **Use multi-stage builds**       | Separe o ambiente de build do de execução, copiando só o necessário.                  |
| **Mantenha imagens atualizadas** | Use versões recentes para aproveitar melhorias de segurança e desempenho.             |

### Exemplo de `.dockerignore`

```
node_modules
npm-debug.log
.git
.env
*.md
```

### Exemplo de Multi-Stage Build

```dockerfile
# ── Etapa 1: Build ──────────────────────────────────────
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# ── Etapa 2: Produção ────────────────────────────────────
FROM node:18-alpine
WORKDIR /app
COPY --from=build /app/dist ./dist
COPY --from=build /app/package*.json ./
RUN npm ci --only=production
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

---

## 7. Gerenciamento de Containers

| Comando                                                           | Descrição                                                    |
|-------------------------------------------------------------------|--------------------------------------------------------------|
| `docker run -d --name meu-container -p 3000:3000 minha-aplicacao` | Inicia o container em background com nome e porta definidos. |
| `docker start meu-container`                                      | Inicia um container parado.                                  |
| `docker stop meu-container`                                       | Para o container.                                            |
| `docker rm meu-container`                                         | Remove o container (deve estar parado).                      |
| `docker exec -it meu-container bash`                              | Abre terminal interativo dentro do container.                |
| `docker logs meu-container`                                       | Exibe os logs do container.                                  |
| `docker inspect meu-container`                                    | Exibe detalhes completos do container.                       |
| `docker images`                                                   | Lista as imagens disponíveis.                                |
| `docker rmi minha-aplicacao`                                      | Remove a imagem (não pode estar em uso).                     |
| `docker system prune -a`                                          | Remove containers parados e imagens não utilizadas.          |

---

## 8. Portas

| Método                           | Comando / Instrução                       | Descrição                                             |
|----------------------------------|-------------------------------------------|-------------------------------------------------------|
| Documentar no Dockerfile         | `EXPOSE 3000`                             | Apenas documenta a porta; não a publica no host.      |
| Porta fixa                       | `docker run -p 3000:3000 minha-aplicacao` | Mapeia a porta 3000 do container para a 3000 do host. |
| Porta diferente no host          | `docker run -p 8080:3000 minha-aplicacao` | Mapeia a porta 3000 do container para a 8080 do host. |
| Porta dinâmica                   | `docker run -P minha-aplicacao`           | Docker escolhe portas aleatórias disponíveis no host. |
| Verificar portas mapeadas        | `docker ps`                               | Coluna `PORTS` mostra todos os mapeamentos ativos.    |
| Verificar portas de um container | `docker port <container>`                 | Lista as portas mapeadas para o container.            |

---

## 9. Volumes

### Conceitos

| Tipo               | Descrição                                                                             |
|--------------------|---------------------------------------------------------------------------------------|
| **Volume nomeado** | Gerenciado pelo Docker; ideal para persistência de dados em produção.                 |
| **Bind mount**     | Mapeia um diretório do host diretamente para o container; ideal para desenvolvimento. |
| **Volume anônimo** | Criado automaticamente; sem nome definido, descartado ao remover o container.         |

### Comandos

| Comando                                                 | Descrição                                                 |
|---------------------------------------------------------|-----------------------------------------------------------|
| `docker volume create meu-volume`                       | Cria um volume nomeado.                                   |
| `docker volume ls`                                      | Lista todos os volumes.                                   |
| `docker volume rm meu-volume`                           | Remove um volume (não pode estar em uso).                 |
| `docker volume prune`                                   | Remove todos os volumes não utilizados.                   |
| `docker volume prune -f`                                | Remove volumes não utilizados sem pedir confirmação.      |
| `docker run -v meu-volume:/app/data minha-aplicacao`    | Monta um volume nomeado dentro do container.              |
| `docker run -v /path/no/host:/app/data minha-aplicacao` | Bind mount: sincroniza diretório do host com o container. |
| `docker inspect <container>`                            | Seção `Mounts` exibe os volumes montados.                 |
| `docker ps -a --filter volume=meu-volume`               | Lista containers que usam o volume especificado.          |

> ⚠️ **Atenção:** `docker volume prune` é irreversível. Confirme que os dados não são necessários antes de executar.

---

## 10. Copiando Arquivos

### Comandos

| Comando                                                      | Descrição                                           |
|--------------------------------------------------------------|-----------------------------------------------------|
| `docker cp arquivo.txt meu-container:/app/arquivo.txt`       | Copia arquivo do host para dentro do container.     |
| `docker cp meu-container:/app/arquivo.txt ./arquivo.txt`     | Copia arquivo de dentro do container para o host.   |
| `docker cp meu-diretorio meu-container:/app/meu-diretorio`   | Copia diretório do host para dentro do container.   |
| `docker cp meu-container:/app/meu-diretorio ./meu-diretorio` | Copia diretório de dentro do container para o host. |
| `docker exec -it meu-container ls /app`                      | Verifica arquivos dentro do container.              |

### Verificando arquivos no host

```bash
# Verificar se o arquivo foi copiado corretamente
ls ./arquivo.txt
```

> 💡 **Dica:** Para desenvolvimento, prefira **bind mounts** (`-v /path/host:/app/data`) em vez de `docker cp`. Assim, as alterações no host são refletidas imediatamente no container sem necessidade de cópia manual.

---

## 11. Redes (Networks)

### Tipos de Rede

| Driver | Descrição |
|--------|-----------|
| `bridge` | Padrão. Rede isolada; containers se comunicam entre si pelo nome. |
| `host` | Compartilha a rede do host diretamente com o container. |
| `none` | Sem rede; container completamente isolado. |
| `overlay` | Permite comunicação entre containers em múltiplos hosts (Docker Swarm). |

### Comandos Básicos

| Comando | Descrição |
|---------|-----------|
| `docker network ls` | Lista todas as redes Docker disponíveis. |
| `docker network ls --filter driver=<driver>` | Lista redes filtrando por driver (ex: `bridge`, `host`, `overlay`). |
| `docker network create <nome>` | Cria uma nova rede Docker (driver `bridge` por padrão). |
| `docker network rm <nome>` | Remove uma rede Docker (não pode estar em uso). |
| `docker network prune` | Remove todas as redes não utilizadas. |
| `docker network inspect <rede>` | Exibe detalhes completos sobre a rede (containers, configurações, IPs). |
| `docker run --network <rede> <imagem>` | Inicia um container conectado a uma rede específica. |
| `docker network connect <rede> <container>` | Conecta um container em execução a uma rede existente. |
| `docker network disconnect <rede> <container>` | Desconecta um container de uma rede. |

### Inspecionando Containers em uma Rede

| Comando | Descrição |
|---------|-----------|
| `docker network inspect <rede> --format '{{json .Containers}}' \| jq .` | Lista containers na rede em JSON formatado. |
| `docker network inspect <rede> --format '{{range .Containers}}{{.Name}} {{end}}'` | Lista apenas os **nomes** dos containers na rede. |
| `docker network inspect <rede> --format '{{range .Containers}}{{.IPv4Address}} {{end}}'` | Lista apenas os **endereços IP** dos containers na rede. |
| `docker network inspect <rede> --format '{{range .Containers}}{{.Name}}: {{.IPv4Address}}{{"\n"}}{{end}}'` | Lista nome e IP de cada container na rede. |

### Testando Conectividade de Rede

Para obter o IP de um container específico e testá-lo, encadeie os comandos:

```bash
# Obter o IP de um container específico (sem a máscara de sub-rede)
docker network inspect <rede> \
  --format '{{range .Containers}}{{.Name}}: {{.IPv4Address}}{{"\n"}}{{end}}' \
  | grep <nome-container> \
  | awk '{print $2}' \
  | cut -d '/' -f 1
```

| Ferramenta | Comando | Descrição |
|------------|---------|-----------|
| `ping` | `ping -c 4 <IP>` | Verifica conectividade básica (ICMP). |
| `curl` | `curl http://<IP>:<porta>` | Testa acesso HTTP a um serviço no container. |
| `netcat` | `nc -zv <IP> <porta>` | Testa se uma porta TCP está aberta. |
| `telnet` | `telnet <IP> <porta>` | Testa conexão interativa em uma porta. |
| `traceroute` | `traceroute <IP>` | Rastreia a rota de rede até o container. |

> 💡 **Dica:** Em redes `bridge` personalizadas, os containers se comunicam pelo **nome do container** como hostname, sem precisar conhecer o IP. Ex: `curl http://meu-container:3000`

> ⚠️ **Atenção:** Na rede `bridge` padrão (`docker0`), a resolução por nome **não** funciona automaticamente — crie sempre redes customizadas para comunicação entre containers.

---

*Referência: [Documentação oficial do Docker](https://docs.docker.com)*


