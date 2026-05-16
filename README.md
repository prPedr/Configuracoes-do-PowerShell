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

Passo 4: Editar o Perfil e colar o código
Abra o arquivo recém-criado no seu editor de código favorito. Se estiver usando o VS Code, basta rodar:

PowerShell
code $PROFILE
Substitua todo o conteúdo do arquivo pelo código abaixo e salve (Ctrl+S).

PowerShell
# 1. Remove o alias padrão para que a nossa função 'ls' funcione
if (Test-Path Alias:\ls) { Remove-Item Alias:\ls -Force }
 
# --- CONFIGURAÇÕES DE INTERFACE (PSReadLine & Erros) ---
# Syntax Highlighting (Escala Soft Dark / Deep Blue)
Set-PSReadLineOption -Colors @{
    Command            = "`e[38;2;137;180;250m" # Soft Blue
    Parameter          = "`e[38;2;116;199;236m" # Sapphire
    Operator           = "`e[38;2;148;226;213m" # Teal
    Variable           = "`e[38;2;137;220;235m" # Sky
    String             = "`e[38;2;166;227;161m" # Green
    Number             = "`e[38;2;250;179;135m" # Peach
    Member             = "`e[38;2;137;180;250m" # Soft Blue
}
 
# Personalizar cores de erro
$PSStyle.Formatting.Error = "`e[38;2;243;139;168m"       # Texto em Maroon
$PSStyle.Formatting.ErrorAccent = "`e[1;38;2;250;179;135m" # Detalhes em Peach
 
# --- FUNÇÃO PING AVANÇADA (Com captura de Ctrl+C) ---
function ping {
    $pingArgs = $args
    $esc = [char]27
    $reset = "$esc[0m"
    $cyan = "$esc[36m"
    $green = "$esc[32m"
    $yellow = "$esc[33m"
    $blue = "$esc[34m"
 
    function Format-PingLine($line) {
        $line = $line -replace '(\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})', "$cyan`$1$reset"
        $line = $line -replace '(bytes=\d+)', "$green`$1$reset"
        $line = $line -replace '(tempo[=<]\d+ms)', "$yellow`$1$reset"
        $line = $line -replace '(TTL=\d+)', "$blue`$1$reset"
        $line = $line -replace '(Enviados = \d+|Recebidos = \d+|Perdidos = \d+)', "$green`$1$reset"
        $line = $line -replace '(Mínimo = \d+ms|Máximo = \d+ms|Média = \d+ms)', "$yellow`$1$reset"
        $line = $line -replace '(\d+% de perda)', "$blue`$1$reset"
        return $line
    }
 
    # Carrega a função GenerateConsoleCtrlEvent para mandar Ctrl+C controlado
    Add-Type -TypeDefinition @"
using System;
using System.Runtime.InteropServices;
public class ConsoleHelper {
    [DllImport("kernel32.dll")]
    public static extern bool GenerateConsoleCtrlEvent(uint dwCtrlEvent, uint dwProcessGroupId);
    [DllImport("kernel32.dll")]
    public static extern bool SetConsoleCtrlHandler(IntPtr handlerRoutine, bool add);
}
"@
 
    $psi = New-Object System.Diagnostics.ProcessStartInfo
    $psi.FileName = "ping.exe"
    $psi.Arguments = $pingArgs -join " "
    $psi.RedirectStandardOutput = $true
    $psi.UseShellExecute = $false
    $psi.CreateNoWindow = $false
 
    $process = [System.Diagnostics.Process]::Start($psi)
 
    # Registra handler para interceptar Ctrl+C no PowerShell
    [Console]::TreatControlCAsInput = $false
    $cancelSource = New-Object System.Threading.CancellationTokenSource
 
    try {
        while (-not $process.StandardOutput.EndOfStream -and -not $cancelSource.Token.IsCancellationRequested) {
            if ([Console]::KeyAvailable) {
                $key = [Console]::ReadKey($true)
                if ($key.Key -eq 'C' -and $key.Modifiers -eq 'Control') {
                    [ConsoleHelper]::SetConsoleCtrlHandler([IntPtr]::Zero, $true) | Out-Null
                    [ConsoleHelper]::GenerateConsoleCtrlEvent(0, 0) | Out-Null
                    Start-Sleep -Milliseconds 50000 
                    [ConsoleHelper]::SetConsoleCtrlHandler([IntPtr]::Zero, $false) | Out-Null
                    $cancelSource.Cancel()
                }
            }
 
            if ($process.StandardOutput.Peek() -ge 0) {
                $line = $process.StandardOutput.ReadLine()
                Write-Host (Format-PingLine $line)
            }
        }
    } finally {
        if (-not $process.HasExited) {
            $process.WaitForExit(2000) | Out-Null
        }
 
        $remaining = $process.StandardOutput.ReadToEnd()
        foreach ($line in ($remaining -split "`n")) {
            if ($line.Trim() -ne "") {
                Write-Host (Format-PingLine $line.TrimEnd())
            }
        }
 
        $process.Dispose()
    }
}
 
# --- FUNÇÃO LS PERSONALIZADA ---
function ls {
    $esc = [char]27
    $reset = "$esc[0m"
    Write-Host "`n$esc[1;38;2;186;194;222mMode      Data         Hora    Tamanho   Nome$reset"
    Write-Host "$esc[38;2;88;91;112m----      ----         ----    -------   ----$reset"
 
    Get-ChildItem @args | ForEach-Object {
        $item = $_
        
        $modeColor = "$esc[38;2;108;112;134m"
        $dateColor = "$esc[38;2;148;226;213m"
        $timeColor = "$esc[38;2;116;199;236m"
        $sizeColor = "$esc[38;2;166;227;161m"
        
        $ext = $item.Extension.ToLower()
        $nameColor = "$reset"
 
        if ($item.PSIsContainer) {
            $nameColor = "$esc[1;38;2;137;180;250m" # Bold Blue (Pastas)
        } else {
            switch ($ext) {
                ".js"   { $nameColor = "$esc[38;2;249;226;175m" } 
                ".ts"   { $nameColor = "$esc[38;2;30;102;245m" }  
                ".tsx"  { $nameColor = "$esc[38;2;30;102;245m" }  
                ".go"   { $nameColor = "$esc[38;2;137;220;235m" } 
                ".py"   { $nameColor = "$esc[38;2;116;199;236m" } 
                ".html" { $nameColor = "$esc[38;2;235;160;172m" } 
                ".css"  { $nameColor = "$esc[38;2;137;180;250m" } 
                ".json" { $nameColor = "$esc[38;2;148;226;213m" } 
                ".md"   { $nameColor = "$esc[38;2;186;194;222m" } 
            }
        }
 
        $dateStr = $item.LastWriteTime.ToString("dd/MM/yyyy")
        $timeStr = $item.LastWriteTime.ToString("HH:mm")
        $mode = $item.Mode.PadRight(10)
        $size = if ($item.PSIsContainer) { "      --" } else { $item.Length.ToString().PadLeft(9) }
 
        Write-Host "$modeColor$mode" -NoNewline
        Write-Host "$dateColor$dateStr  " -NoNewline
        Write-Host "$timeColor$timeStr  " -NoNewline
        Write-Host "$sizeColor$size  " -NoNewline
        Write-Host " $nameColor$($item.Name)$reset"
    }
    Write-Host ""
}
Passo 5: Reiniciar o Terminal
Feche o seu Windows Terminal completamente e abra novamente. Pronto! Teste os comandos ls em uma pasta com código e faça um ping 8.8.8.8 para ver a mágica acontecendo.

PowerShell
if (!(Test-Path -Path $PROFILE)) { New-Item -ItemType File -Path $PROFILE -Force }
