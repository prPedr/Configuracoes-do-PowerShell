# 💻 Windows Terminal & PowerShell Custom Setup

Este repositório contém as minhas configurações completas para o **Windows Terminal** e **PowerShell 7**. O ambiente foi desenhado para ser minimalista, produtivo e agradável aos olhos, unindo um tema inspirado no *Catppuccin Mocha* para o terminal com um script personalizado de *Soft Dark & Deep Blue* para o PowerShell.

## ✨ Funcionalidades

* **Tema Customizado:** Baseado no Catppuccin Mocha, mas com um fundo ainda mais escuro e limpo (`#13131C`).
* **Fonte Otimizada:** Utiliza a *JetBrains Mono* com ligaturas habilitadas para melhor legibilidade de código.
* **Syntax Highlighting Automático:** Cores agradáveis no PowerShell enquanto você digita os comandos.
* **Função `ls` Inteligente:** Saída colorida mapeada para destacar pastas e extensões específicas de desenvolvimento (`.ts`, `.go`, `.tsx`, `.py`, `.js`, etc.).
* **Função `ping` Avançada:** O comando `ping` ganha cores para facilitar a leitura e intercepta o `Ctrl+C` perfeitamente, exibindo as estatísticas finais antes de encerrar.

---

## 🛠️ Pré-requisitos

Antes de aplicar as configurações, certifique-se de ter:
1. [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701) instalado.
2. [PowerShell 7](https://learn.microsoft.com/pt-br/powershell/scripting/install/installing-powershell-on-windows) instalado (versão mais recente, diferente do Windows PowerShell padrão).
3. Fonte [JetBrains Mono](https://www.jetbrains.com/lp/mono/) instalada no seu Windows.

---

## 🚀 Como instalar e usar

Siga o passo a passo abaixo para aplicar essa customização no seu próprio ambiente.

### Passo 1: Configurando o Windows Terminal

Vamos aplicar o tema e as configurações de fonte e atalhos no seu Windows Terminal.

1. Abra o Windows Terminal.
2. Pressione `Ctrl + ,` (vírgula) para abrir as Configurações.
3. No canto inferior esquerdo, clique em **Abrir arquivo JSON** (ícone de engrenagem).
4. Substitua o conteúdo do seu arquivo pelo código abaixo e salve (`Ctrl + S`):

<details>
<summary><b>Clique aqui para expandir o código do settings.json</b></summary>

```json
{
    "$help": "[https://aka.ms/terminal-documentation](https://aka.ms/terminal-documentation)",
    "$schema": "[https://aka.ms/terminal-profiles-schema](https://aka.ms/terminal-profiles-schema)",
    "actions": [],
    "copyFormatting": "none",
    "copyOnSelect": false,
    "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
    "keybindings": [
        {
            "id": "Terminal.PasteFromClipboard",
            "keys": "ctrl+v"
        },
        {
            "id": "Terminal.CopyToClipboard",
            "keys": "ctrl+c"
        }
    ],
    "newTabMenu": [
        {
            "type": "remainingProfiles"
        }
    ],
    "profiles": {
        "defaults": {
            "antialiasingMode": "cleartype",
            "colorScheme": "Catppuccin Mocha",
            "cursorColor": "#F5E0DC",
            "cursorShape": "bar",
            "font": {
                "face": "JetBrains Mono",
                "features": {
                    "calt": 1
                },
                "size": 11
            },
            "opacity": 100,
            "padding": "12",
            "useAcrylic": false
        },
        "list": [
            {
                "commandline": "pwsh.exe",
                "experimental.retroTerminalEffect": false,
                "font": {
                    "weight": "normal"
                },
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "intenseTextStyle": "bright",
                "name": "PowerShell 7",
                "opacity": 100,
                "scrollbarState": "visible",
                "selectionBackground": "#585B70",
                "source": "Windows.Terminal.PowershellCore"
            },
            {
                "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "Windows PowerShell"
            },
            {
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "Command Prompt"
            }
        ]
    },
    "schemes": [
        {
            "background": "#13131C",
            "black": "#45475A",
            "blue": "#2C58A3",
            "brightBlack": "#C191F2",
            "brightBlue": "#2C58A3",
            "brightCyan": "#94E2D5",
            "brightGreen": "#A6E3A1",
            "brightPurple": "#F5C2E7",
            "brightRed": "#F38BA8",
            "brightWhite": "#A6ADC8",
            "brightYellow": "#F9E2AF",
            "cursorColor": "#F5E0DC",
            "cyan": "#94E2D5",
            "foreground": "#CDD6F4",
            "green": "#A6E3A1",
            "name": "Catppuccin Mocha",
            "purple": "#CBA6F7",
            "red": "#F38BA8",
            "selectionBackground": "#585B70",
            "white": "#BAC2DE",
            "yellow": "#F9E2AF"
        }
    ],
    "themes": []
}

```


Passo 2: Liberar a execução de scripts no PowerShell
Por padrão, o Windows bloqueia a execução de scripts personalizados. Abra o seu PowerShell como Administrador e rode o comando abaixo:

PowerShell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Pressione S (ou Y) quando for solicitado para confirmar.

Passo 3: Criar o arquivo de Perfil do PowerShell
Agora, você precisa criar o arquivo de configuração do seu terminal. Abra um PowerShell normal (sem ser administrador) e rode:

PowerShell
if (!(Test-Path -Path $PROFILE)) { New-Item -ItemType File -Path $PROFILE -Force }


