# 🐳 Comandos Docker Compose

> Referência completa de comandos e conceitos do Docker Compose.

---

## 📑 Índice

- [docker compose up](#-docker-compose-up)
- [docker compose down](#-docker-compose-down)
- [docker compose build](#-docker-compose-build)
- [docker compose start / stop / restart](#-start-stop-e-restart)
- [docker compose ps](#-docker-compose-ps)
- [docker compose logs](#-docker-compose-logs)
- [docker compose exec](#-docker-compose-exec)
- [docker compose scale / pull / push](#-escala-imagens-e-registro)
- [docker compose config / version / help](#-utilitários)
- [Redes e Networking](#-redes-e-networking)

---

## 🚀 docker compose up

Levanta os serviços definidos no arquivo `docker-compose.yml`. Se os contêineres não existirem, eles serão criados.

### Opções básicas

| Comando | Descrição |
|---|---|
| `docker compose up` | Levanta os serviços. Cria os contêineres se não existirem. |
| `docker compose up -d` | Levanta os serviços em segundo plano (**detached mode**). |
| `docker compose up --build` | Levanta os serviços, construindo as imagens se necessário. |
| `docker compose up --force-recreate` | Recria os contêineres mesmo sem mudanças na configuração. |
| `docker compose up --no-deps` | Levanta os serviços sem iniciar os serviços dependentes. |
| `docker compose up --remove-orphans` | Levanta os serviços e remove contêineres órfãos não definidos no `docker-compose.yml`. |
| `docker compose up --scale <serviço>=<n>` | Levanta os serviços com `n` réplicas do serviço especificado. |
| `docker compose up -f <arquivo>` | Usa um arquivo `docker-compose.yml` específico. |

### Combinações de flags

```bash
# Builda e recria contêineres
docker compose up --build --force-recreate

# Builda sem subir dependências
docker compose up --build --no-deps

# Builda e remove órfãos
docker compose up --build --remove-orphans

# Recria sem subir dependências
docker compose up --force-recreate --no-deps

# Recria e remove órfãos
docker compose up --force-recreate --remove-orphans

# Sem dependências e remove órfãos
docker compose up --no-deps --remove-orphans

# Builda, recria e sem dependências
docker compose up --build --force-recreate --no-deps

# Builda, recria e remove órfãos
docker compose up --build --force-recreate --remove-orphans

# Builda, sem dependências e remove órfãos
docker compose up --build --no-deps --remove-orphans

# Recria, sem dependências e remove órfãos
docker compose up --force-recreate --no-deps --remove-orphans

# Todas as flags combinadas
docker compose up --build --force-recreate --no-deps --remove-orphans

# Usando arquivo específico com build
docker compose up --build -f docker-compose.prod.yml
```

> **Dica:** Use `-d` em conjunto com qualquer uma das flags acima para rodar em background. Ex: `docker compose up -d --build`

---

## 🛑 docker compose down

Para e remove os contêineres e recursos criados pelo `docker compose up`.

| Comando | Descrição |
|---|---|
| `docker compose down` | Para e remove contêineres e redes. |
| `docker compose down --volumes` | Também remove os volumes associados. |
| `docker compose down --rmi all` | Também remove as imagens utilizadas. |
| `docker compose down --remove-orphans` | Também remove contêineres órfãos não definidos no `docker-compose.yml`. |

```bash
# Exemplo: parar tudo e limpar volumes e imagens
docker compose down --volumes --rmi all --remove-orphans
```

---

## 🔨 docker compose build

Constrói ou reconstrói as imagens dos serviços definidos no `docker-compose.yml`.

```bash
docker compose build

# Construir sem usar cache
docker compose build --no-cache

# Construir um serviço específico
docker compose build <serviço>
```

---

## ▶️ Start, Stop e Restart

| Comando | Descrição |
|---|---|
| `docker compose start` | Inicia os contêineres que estão parados. |
| `docker compose stop` | Para os contêineres em execução, sem removê-los. |
| `docker compose restart` | Reinicia os contêineres em execução. |

```bash
# Parar apenas um serviço específico
docker compose stop <serviço>

# Reiniciar apenas um serviço específico
docker compose restart <serviço>
```

---

## 📋 docker compose ps

Lista os contêineres gerenciados pelo Compose e seus status.

```bash
docker compose ps

# Exibir apenas os IDs dos contêineres
docker compose ps -q
```

---

## 📄 docker compose logs

Exibe os logs dos contêineres em execução.

### Opções disponíveis

| Comando | Descrição |
|---|---|
| `docker compose logs` | Exibe todos os logs. |
| `docker compose logs -f` | Exibe logs em tempo real (**follow mode**). |
| `docker compose logs --tail <n>` | Exibe apenas as últimas `n` linhas. |
| `docker compose logs --no-color` | Exibe logs sem colorização. |
| `docker compose logs --timestamps` | Exibe logs com timestamps. |
| `docker compose logs --details` | Exibe logs com detalhes adicionais (nome do serviço, ID do contêiner). |

### Exemplos

```bash
# Seguir logs mostrando apenas as últimas 100 linhas
docker compose logs --follow --tail 100

# Logs em tempo real com timestamps e sem cores
docker compose logs -f --timestamps --no-color

# Logs de um serviço específico
docker compose logs <serviço>

# Logs em tempo real de um serviço específico
docker compose logs -f <serviço>
```

---

## 💻 docker compose exec

Executa um comando dentro de um contêiner em execução.

### Opções disponíveis

| Flag | Descrição |
|---|---|
| `-T` | Desabilita a alocação de pseudo-TTY. |
| `--user <usuário>` | Executa o comando como um usuário específico. |
| `--workdir <diretório>` | Define o diretório de trabalho dentro do contêiner. |
| `--env <var>=<valor>` | Define uma variável de ambiente para o comando. |
| `--env-file <arquivo>` | Carrega variáveis de ambiente a partir de um arquivo. |
| `--privileged` | Executa o comando com privilégios elevados. |

### Exemplos

```bash
# Acessar o terminal do contêiner do serviço web
docker compose exec web bash

# Executar comando sem TTY (ideal para scripts)
docker compose exec -T web ls

# Executar como usuário específico
docker compose exec --user www-data web bash

# Executar com diretório de trabalho específico
docker compose exec --workdir /app web bash

# Executar com variável de ambiente
docker compose exec --env DEBUG=true web bash

# Carregar variáveis de ambiente de um arquivo
docker compose exec --env-file .env web bash

# Executar com privilégios elevados
docker compose exec --privileged web bash

# Combinar usuário e diretório de trabalho
docker compose exec --user www-data --workdir /app web bash

# Combinar usuário e variável de ambiente
docker compose exec --user www-data --env DEBUG=true web bash

# Combinar diretório de trabalho e variável de ambiente
docker compose exec --workdir /app --env DEBUG=true web bash

# Combinar todas as opções
docker compose exec --user www-data --workdir /app --env DEBUG=true web bash
```

---

## 📦 Escala, Imagens e Registro

| Comando | Descrição |
|---|---|
| `docker compose scale <serviço>=<n>` | Escala um serviço para `n` contêineres *(deprecated, use `--scale` no `up`)*. |
| `docker compose pull` | Baixa as imagens mais recentes para os serviços definidos. |
| `docker compose push` | Envia as imagens dos serviços para um registro (ex: Docker Hub). |

```bash
# Escalar ao subir (forma recomendada)
docker compose up --scale web=3 -d

# Baixar imagens sem iniciar os serviços
docker compose pull

# Enviar imagens para o registro
docker compose push
```

---

## 🛠️ Utilitários

| Comando | Descrição |
|---|---|
| `docker compose config` | Valida e exibe a configuração final do `docker-compose.yml`. |
| `docker compose version` | Exibe a versão do Docker Compose instalada. |
| `docker compose help` | Exibe a ajuda e os comandos disponíveis. |

```bash
docker compose config
docker compose version
docker compose help
```

---

## 🌐 Redes e Networking

A rede padrão do Docker Compose é do tipo **bridge**, onde os contêineres se comunicam entre si usando os nomes dos serviços como hostnames.

### Tipos de Rede

| Tipo | Descrição |
|---|---|
| **bridge** | Rede padrão. Contêineres isolados do host, comunicam-se entre si pelo nome do serviço. |
| **host** | Contêineres compartilham a pilha de rede do host. Sem isolamento de rede. |
| **overlay** | Comunicação entre contêineres em diferentes hosts Docker (requer Docker Swarm). |
| **none** | Sem acesso a rede. Contêiner totalmente isolado. |

### Criando uma Rede Personalizada

Para criar e usar uma rede personalizada no `docker-compose.yml`:

```yaml
version: '3'
services:
  web:
    image: nginx
    networks:
      - my-network
  db:
    image: mysql
    networks:
      - my-network

networks:
  my-network:
```

> Nesse exemplo, os contêineres `web` e `db` estão na mesma rede e podem se comunicar usando os nomes dos serviços como hostnames (ex: `web` acessa o banco em `db:3306`).

### Conectando um Contêiner a uma Rede Existente

```bash
docker network connect my-network my-container
```

### Desconectando um Contêiner de uma Rede

```bash
docker network disconnect my-network my-container
```

### Listando Redes Disponíveis

```bash
docker network ls
```

### Inspecionando uma Rede

```bash
docker network inspect my-network
```
