# Tutorial: Oh My Posh + Autocomplete no Windows

> Guia para configurar um terminal bonito e com autocomplete inteligente no **PowerShell** e no **Git Bash**.

---

## Índice

- [Pré-requisitos](#pré-requisitos)
- [Parte 1 — Instalação do Oh My Posh](#parte-1--instalação-do-oh-my-posh)
- [Parte 2 — Configuração no PowerShell](#parte-2--configuração-no-powershell)
- [Parte 3 — Configuração no Git Bash](#parte-3--configuração-no-git-bash)
- [Parte 4 — Instalar uma Nerd Font](#parte-4--instalar-uma-nerd-font)
- [Parte 5 — Configurar a fonte no Windows Terminal](#parte-5--configurar-a-fonte-no-windows-terminal)
- [Referência rápida de atalhos](#referência-rápida-de-atalhos)

---

## Pré-requisitos

- Windows 10 ou superior
- [Windows Terminal](https://aka.ms/terminal) (recomendado — instale pela Microsoft Store)
- PowerShell 5.1+ ou PowerShell 7+
- Git for Windows instalado (para o Git Bash)

---

## Parte 1 — Instalação do Oh My Posh

Abra o **PowerShell** e execute:

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

Após a instalação, **feche e reabra o terminal** para o PATH ser atualizado.

Verifique se instalou corretamente:

```powershell
oh-my-posh --version
```

---

## Parte 2 — Configuração no PowerShell

### 2.1 Atualizar o PSReadLine

O autocomplete inteligente requer PSReadLine **2.2 ou superior**. Verifique sua versão:

```powershell
Get-Module PSReadLine -ListAvailable
```

Se a versão for menor que 2.2, atualize:

```powershell
Install-Module PSReadLine -Force -SkipPublisherCheck -Scope AllUsers
```

> Se pedir confirmação de repositório, digite `A` (Yes to All).

**Feche e reabra o terminal** após a instalação.

### 2.2 Editar o perfil do PowerShell

Abra o arquivo de perfil:

```powershell
notepad $PROFILE
```

Se o arquivo não existir, crie-o primeiro:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

Adicione o seguinte conteúdo ao arquivo:

```powershell
# Forçar uso da versão atualizada do PSReadLine
Import-Module PSReadLine -RequiredVersion 2.4.5

# Inicializar Oh My Posh
oh-my-posh init pwsh | Invoke-Expression

# Autocomplete inteligente com histórico
Set-PSReadLineOption -PredictionSource History
Set-PSReadLineOption -PredictionViewStyle ListView
```

> **Dica:** Se não souber qual versão do PSReadLine foi instalada, substitua `2.4.5` pelo número que apareceu no comando `Get-Module PSReadLine -ListAvailable`.

Salve o arquivo e recarregue o perfil:

```powershell
. $PROFILE
```

### 2.3 Como usar o autocomplete no PowerShell

| Ação                            | Tecla                      |
|---------------------------------|----------------------------|
| Completar arquivo/comando       | `Tab`                      |
| Ver sugestões em lista          | `↓` após começar a digitar |
| Aceitar sugestão inline         | `→`                        |
| Navegar pela lista de sugestões | `↑` / `↓`                  |
| Fechar lista de sugestões       | `Esc`                      |

---

## Parte 3 — Configuração no Git Bash

### 3.1 Editar o arquivo `.bashrc`

Abra o arquivo de perfil do Git Bash:

```bash
notepad ~/.bashrc
```

Se não existir, ele será criado automaticamente. Adicione o seguinte conteúdo:

```bash
# Inicializar Oh My Posh
eval "$(oh-my-posh init bash)"

# Ativar autocomplete
source /usr/share/bash-completion/bash_completion 2>/dev/null || true
```

Salve o arquivo e recarregue:

```bash
source ~/.bashrc
```

### 3.2 Como usar o autocomplete no Git Bash

| Ação                            | Tecla                |
|---------------------------------|----------------------|
| Completar arquivo/comando       | `Tab`                |
| Ver todas as opções disponíveis | `Tab` `Tab`          |
| Completar subcomandos do git    | `git ` + `Tab` `Tab` |
| Navegar pelo histórico          | `↑` / `↓`            |
| Buscar no histórico             | `Ctrl + R`           |

---

## Parte 4 — Instalar uma Nerd Font

O Oh My Posh usa ícones especiais que requerem uma **Nerd Font**. Sem ela, aparecerão caracteres estranhos como `?` ou quadradinhos.

No **PowerShell**, execute:

```powershell
oh-my-posh font install
```

Uma lista interativa aparecerá. Fontes recomendadas:

- `Meslo` — mais popular, ótima legibilidade
- `CascadiaCode` — fonte oficial da Microsoft, visual moderno
- `FiraCode` — muito usada por desenvolvedores

Use as setas para navegar e `Enter` para instalar.

---

## Parte 5 — Configurar a fonte no Windows Terminal

Após instalar a Nerd Font, configure-a no Windows Terminal:

1. Abra o Windows Terminal
2. Pressione `Ctrl + ,` para abrir as **Configurações**
3. No painel esquerdo, clique no perfil desejado (ex: **PowerShell** ou **Git Bash**)
4. Clique em **Aparência**
5. Em **Tipo de fonte**, selecione a Nerd Font instalada (ex: `MesloLGM Nerd Font`)
6. Clique em **Salvar**

### Para o Git Bash fora do Windows Terminal

1. Clique com botão direito na barra de título do Git Bash
2. Vá em **Options** → **Text**
3. Troque a fonte para a Nerd Font instalada
4. Clique em **Apply**

---

## Referência rápida de atalhos

### PowerShell

| Ação                            | Tecla      |
|---------------------------------|------------|
| Autocomplete                    | `Tab`      |
| Sugestão inline (aceitar)       | `→`        |
| Lista de sugestões do histórico | `↓`        |
| Navegar no histórico            | `↑` / `↓`  |
| Limpar tela                     | `Ctrl + L` |
| Cancelar comando atual          | `Ctrl + C` |

### Git Bash

| Ação                   | Tecla       |
|------------------------|-------------|
| Autocomplete           | `Tab`       |
| Ver todas as opções    | `Tab` `Tab` |
| Histórico anterior     | `↑`         |
| Buscar no histórico    | `Ctrl + R`  |
| Limpar tela            | `Ctrl + L`  |
| Cancelar comando atual | `Ctrl + C`  |

---

## Solução de problemas

**Ícones aparecem como `?` ou quadradinhos**
→ A Nerd Font não está configurada. Siga a [Parte 4](#parte-4--instalar-uma-nerd-font) e a [Parte 5](#parte-5--configurar-a-fonte-no-windows-terminal).

**Erro `PredictionSource` não encontrado**
→ O PSReadLine está desatualizado. Siga o passo [2.1](#21-atualizar-o-psreadline).

**Oh My Posh não é reconhecido no Git Bash**
→ Verifique se o Oh My Posh está no PATH. Execute `where oh-my-posh` no PowerShell para confirmar o caminho.

**O perfil do PowerShell não carrega**
→ Verifique a política de execução:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```