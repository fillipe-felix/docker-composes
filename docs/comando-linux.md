# 📋 Comandos Linux — Referência Rápida

---

## 👤 Informações do Sistema

| Comando | Descrição |
|---------|-----------|
| `whoami` | Mostra qual usuário está logado no sistema |
| `echo mensagem` | Exibe uma mensagem na tela |
| `echo $0` | Exibe o nome do shell/comando sendo executado |

---

## 📦 Gerenciamento de Pacotes (APT)

| Comando | Descrição |
|---------|-----------|
| `apt list` | Exibe os pacotes disponíveis para instalação |
| `apt list --installed` | Exibe os pacotes instalados no sistema |
| `apt update` | Atualiza a lista de pacotes disponíveis |
| `apt install <pacote>` | Instala um pacote (ex: `apt install nano`) |
| `apt remove <pacote>` | Remove um pacote (ex: `apt remove nano`) |

---

## 📝 Editor de Texto Nano

| Comando | Descrição |
|---------|-----------|
| `nano` | Abre o editor de texto no terminal |
| `nano <arquivo>` | Abre um arquivo para edição |
| `nano -w <arquivo>` | Abre o arquivo sem quebra de linha automática |

---

## 🗂️ Navegação de Arquivos

| Comando | Descrição |
|---------|-----------|
| `pwd` | Mostra o caminho do diretório atual |
| `ls` | Lista os arquivos e pastas do diretório atual |
| `ls -1` | Lista em uma coluna |
| `ls -l` | Lista com detalhes (permissões, tamanho, data) |
| `ls -a` | Lista incluindo arquivos ocultos |
| `cd <pasta>` | Muda para a pasta especificada |
| `cd ..` | Volta para a pasta anterior |
| `cd ~` | Vai para a pasta home do usuário |
| `cd /` | Vai para a raiz do sistema de arquivos |

---

## 🛠️ Manipulação de Arquivos

| Comando | Descrição |
|---------|-----------|
| `mkdir <pasta>` | Cria uma nova pasta |
| `rm <arquivo>` | Remove um arquivo |
| `rm -r <pasta>` | Remove uma pasta e todo o seu conteúdo |
| `cp <origem> <destino>` | Copia um arquivo para o destino especificado |
| `mv <origem> <destino>` | Move ou renomeia um arquivo/pasta |
| `touch <arquivo>` | Cria um arquivo vazio ou atualiza a data de modificação |
| `cat <arquivo>` | Exibe o conteúdo de um arquivo |
| `cat <arq1> > <cópia>` | Copia o conteúdo de um arquivo para outro |
| `cat <arq1> >> <cópia>` | Adiciona o conteúdo ao final de outro arquivo |
| `cat <arq1> <arq2> > <novo>` | Combina dois arquivos em um novo |
| `head <arquivo>` | Exibe as primeiras linhas de um arquivo |
| `tail <arquivo>` | Exibe as últimas linhas de um arquivo |

---

## 🔍 Busca de Arquivos

### `find` — Buscar arquivos e pastas

| Comando | Descrição |
|---------|-----------|
| `find <pasta> -name <arquivo>` | Procura por nome dentro da pasta |
| `find <pasta> -type f` | Lista todos os arquivos |
| `find <pasta> -type d` | Lista todas as subpastas |
| `find <pasta> -size +100M` | Arquivos maiores que 100 MB |
| `find <pasta> -mtime -7` | Arquivos modificados nos últimos 7 dias |

### `grep` — Buscar conteúdo dentro de arquivos

| Comando | Descrição |
|---------|-----------|
| `grep <palavra> <arquivo>` | Busca uma palavra em um arquivo |
| `grep -r <palavra> <pasta>` | Busca recursiva em todos os arquivos |
| `grep -i <palavra> <arquivo>` | Busca sem diferenciar maiúsculas/minúsculas |
| `grep -v <palavra> <arquivo>` | Exibe linhas que **não** contêm a palavra |
| `grep -n <palavra> <arquivo>` | Exibe as linhas com seus números |
| `grep -c <palavra> <arquivo>` | Conta quantas linhas contêm a palavra |
| `grep -l <palavra> <pasta>/*` | Lista arquivos que contêm a palavra |
| `grep -r -l <palavra> <pasta>` | Busca recursiva e lista os arquivos encontrados |

---

## 💾 Sistema de Arquivos

| Diretório | Descrição |
|-----------|-----------|
| `/dev` | Arquivos de dispositivos do sistema |
| `/etc` | Arquivos de configuração do sistema |
| `/home` | Pastas dos usuários do sistema |
| `/var` | Arquivos de log e dados variáveis |
| `/media` | Montagem de mídias removíveis (CD, DVD, USB) |
| `/mnt` | Ponto de montagem manual de sistemas de arquivos |
| `/opt` | Programas opcionais instalados manualmente |
| `/proc` | Informações sobre processos e kernel (virtual) |
| `/sys` | Interface com o kernel do sistema |
| `/srv` | Dados de serviços do sistema |
| `/usr` | Programas e bibliotecas do sistema |
| `/boot` | Arquivos de inicialização do sistema |

---

## ⛓️ Encadeamento de Comandos

| Operador | Descrição |
|----------|-----------|
| `cmd1 && cmd2` | Executa `cmd2` **somente se** `cmd1` tiver sucesso |
| `cmd1 \|\| cmd2` | Executa `cmd2` **somente se** `cmd1` falhar |
| `cmd1 ; cmd2` | Executa `cmd2` independentemente do resultado de `cmd1` |

---

## ⚙️ Gerenciamento de Processos

| Comando | Descrição |
|---------|-----------|
| `ps` | Exibe os processos em execução |
| `ps aux` | Exibe todos os processos com detalhes |
| `ps -ef` | Exibe processos com detalhes no formato estendido |
| `kill <PID>` | Termina o processo com o ID especificado |
| `kill -9 <PID>` | Força a terminação do processo |
| `top` | Monitor de processos em tempo real (ordenado por CPU) |
| `htop` | Monitor interativo e mais amigável (requer instalação) |

---

## 👥 Gerenciamento de Usuários

| Comando | Descrição |
|---------|-----------|
| `useradd <usuario>` | Cria um novo usuário |
| `useradd -m <usuario>` | Cria um usuário com pasta home |
| `usermod -aG <grupo> <usuario>` | Adiciona um usuário a um grupo |
| `userdel <usuario>` | Remove um usuário do sistema |
| `passwd <usuario>` | Altera a senha de um usuário |
| `groups <usuario>` | Exibe os grupos do usuário |
| `id <usuario>` | Exibe o ID e grupos do usuário |

---

## 👨‍👩‍👧 Gerenciamento de Grupos

| Comando | Descrição |
|---------|-----------|
| `groupadd <grupo>` | Cria um novo grupo |
| `groupdel <grupo>` | Remove um grupo do sistema |
| `usermod -aG <grupo> <usuario>` | Adiciona um usuário a um grupo |

---

## 🔐 Gerenciamento de Permissões

### `chmod` — Alterar permissões

| Comando | Descrição |
|---------|-----------|
| `chmod 755 <arquivo>` | `rwxr-xr-x` — Proprietário: tudo; Grupo/Outros: ler e executar |
| `chmod 700 <arquivo>` | `rwx------` — Somente o proprietário tem acesso total |
| `chmod 644 <arquivo>` | `rw-r--r--` — Proprietário: ler/escrever; Grupo/Outros: somente ler |
| `chmod 777 <arquivo>` | `rwxrwxrwx` — Todos têm permissão total |
| `chmod u+x <arquivo>` | Adiciona permissão de execução para o proprietário |
| `chmod g-w <arquivo>` | Remove a permissão de escrita do grupo |
| `chmod o+r <arquivo>` | Adiciona permissão de leitura para outros usuários |

### `chown` — Alterar proprietário

| Comando | Descrição |
|---------|-----------|
| `chown <usuario> <arquivo>` | Altera o proprietário do arquivo |
| `chown <usuario>:<grupo> <arquivo>` | Altera o proprietário e o grupo do arquivo |

### Estrutura das Permissões

```
[ proprietário ][ grupo ][ outros ]
     rwx           rwx      rwx
```

| Posição | Representa |
|---------|-----------|
| 1º grupo (bits 1-3) | Permissões do **proprietário** |
| 2º grupo (bits 4-6) | Permissões do **grupo** |
| 3º grupo (bits 7-9) | Permissões dos **outros usuários** |
