---
title: Terminal integrado
titleSuffix: Azure Data Studio
description: Saiba mais sobre o terminal integrado no estúdio de dados do Azure.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 13a0e3c17f45e0ba136d83f832d3531bc8059884
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959532"
---
# <a name="integrated-terminal"></a>Terminal integrado

No [!INCLUDE[name-sos](../includes/name-sos-short.md)], você pode abrir um terminal integrado, inicialmente, começando na raiz do seu espaço de trabalho. Isso pode ser conveniente, pois você não precise alternar windows ou alterar o estado de um terminal existente para executar uma tarefa de linha de comando rápida.

Para abrir o terminal:

* Use o **Ctrl +'** atalho de teclado com o caractere de acento grave.
* Use o **modo de exibição** | **Terminal integrado** comando de menu.
* Dos **paleta de comandos** (**Ctrl + Shift + P**), use o **Terminal integrado do modo de exibição: Ativar/desativar** comando.

![Terminal](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Você ainda pode abrir um shell externo com o Gerenciador **abrir no Prompt de comando** comando (**Open in Terminal** no Mac ou Linux) se você preferir trabalhar fora [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="managing-multiple-terminals"></a>Gerenciando vários terminais

Você pode criar vários terminais aberta para diferentes locais e navegar facilmente entre eles. Terminal instâncias podem ser adicionadas clicando no ícone de adição no canto superior direito do **TERMINAL** do painel ou disparar pela **Ctrl + Shift +'** comando. Isso cria outra entrada na lista suspensa que pode ser usada para alternar entre eles.

![Vários terminais](media/integrated-terminal/terminal-multiple-instances.png)

Podem botão remover instâncias de terminal, pressionando a Lixeira.

> [!TIP]
> Se você usar vários terminais extensivamente, você pode adicionar associações de teclas para a `focusNext`, `focusPrevious` e `kill` comandos descritas a [seção de associações de teclas](#key-bindings) para permitir a navegação entre elas usando apenas o teclado.

## <a name="configuration"></a>Configuração

O shell usado o padrão é `$SHELL` no Linux e macOS, o PowerShell no Windows 10 e cmd.exe em versões anteriores do Windows. Elas podem ser substituídas manualmente, definindo `terminal.integrated.shell.*` na [configurações](settings.md). Argumentos podem ser passados para o shell de terminal no Linux e macOS usando o `terminal.integrated.shellArgs.*` configurações.

### <a name="windows"></a>Windows

Configurar corretamente o seu shell no Windows é uma questão de localizar o executável correto e atualizando a configuração. Veja a seguir uma lista de arquivos executáveis do shell comum e seus locais padrão:

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> Para ser usado como um terminal integrado, o executável de shell deve ser um aplicativo de console, de modo que `stdin/stdout/stderr` podem ser redirecionadas.

> [!TIP]
> O shell de terminal integrado está em execução com as permissões do [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Se você precisar executar um shell de comando com privilégios elevados (administrador) ou permissões diferentes, você pode usar os utilitários de plataforma, como `runas.exe` dentro de um terminal.

### <a name="shell-arguments"></a>Argumentos de shell

Você pode passar argumentos para o shell quando ele é iniciado.

Por exemplo, para habilitar a execução de bash como um shell de logon (que é executado `.bash_profile`), passe o `-l` argumento (com aspas duplas):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>Configurações de exibição de terminal

Você pode personalizar a fonte de terminal integrada e a altura da linha com as seguintes configurações:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>Associações de teclas do Terminal

O **exibição: Ativar/desativar o Terminal integrado** comando é associado ao **Ctrl +'** para alternar rapidamente o painel de terminal integrado dentro e fora do modo de exibição.

Abaixo estão os atalhos de teclado para navegar rapidamente no terminal integrado:

|Chave|Comando|  
|---|---|  
|**CTRL +\`**|Mostrar o terminal integrado|  
|**Ctrl+Shift+\`**|Criar um novo terminal|  
|**CTRL + seta para cima**|Role para cima|  
|**CTRL + seta para baixo**|Role para baixo|  
|**Ctrl+PageUp**|Rola página para cima|  
|**Ctrl+PageDown**|Rolar página para baixo|  
|**CTRL + Home**|Role para cima|  
|**Ctrl+End**|Role para baixo|  
|**Ctrl+K**|Limpar o terminal|  

Outros comandos de terminal estão disponíveis e podem ser associados a seus atalhos de teclado preferencial.

São eles:

* `workbench.action.terminal.focus`: Concentre-se o terminal. Isso é como alternar mas concentra-se o terminal, em vez de ocultá-lo, se ele estiver visível.
* `workbench.action.terminal.focusNext`: Concentra-se a próxima instância de terminal.
* `workbench.action.terminal.focusPrevious`: Concentra-se a instância anterior de terminal.
* `workbench.action.terminal.kill`: Remova a instância atual de terminal.
* `workbench.action.terminal.runSelectedText`: Execute o texto selecionado na instância do terminal.
* `workbench.action.terminal.runActiveFile`: Execute o arquivo de ativo na instância do terminal.

### <a name="run-selected-text"></a>Executar o texto selecionado

Para usar o `runSelectedText` de comando, selecione o texto em um editor e execute o comando **Terminal: Executar o texto selecionado no Active Directory Terminal** por meio de **paleta de comando** (**Ctrl + Shift + P**). O terminal tenta executar o texto selecionado:

![Executar o texto selecionado](media/integrated-terminal/terminal_run_selected.png)

Se nenhum texto estiver selecionado no editor ativo, a linha que o cursor estiver sobre é executada no terminal.

### <a name="copy--paste"></a>Copiar e colar

As associações de teclas para copiar e colar sigam os padrões da plataforma:

* Linux: **Ctrl + Shift + C** e **Ctrl + Shift + V**
* Mac: **Cmd + C** e **Cmd + V**
* Windows: **CTRL + C** e **Ctrl + V**

### <a name="find"></a>Localizar

O Terminal integrado possui funcionalidade de localização básica que pode ser disparada com **Ctrl + F**.

Se você quiser **Ctrl + F** para ir para o shell em vez de iniciar o widget de localização no Linux e Windows, você precisará remover a associação de teclas da seguinte forma:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>Renomear as sessões de terminal

Sessões de Terminal integradas agora podem ser renomeadas usando o **Terminal: Renomeie** (`workbench.action.terminal.rename`) comando. O novo nome é exibido na lista suspensa de seleção terminal.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>Associações de teclas forçando a passagem de terminal

Enquanto o foco está no terminal integrado, muitos associações de teclas não funcionarão porque os pressionamentos de tecla são passados para e consumidos pelo terminal em si. O `terminal.integrated.commandsToSkipShell` configuração pode ser usada para resolver esse problema. Ele contém uma matriz de nomes de comando cujas associações de teclas ignorar o processamento, o shell e em vez disso, ser processadas pelo [!INCLUDE[name-sos](../includes/name-sos-short.md)] sistema de associação de chave. Por padrão, isso inclui todas as associações de teclas terminal além de uma select alguns comumente usados associações de teclas.

