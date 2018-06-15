---
title: Terminal integrado no Studio de operações do SQL (visualização) | Microsoft Docs
description: Saiba mais sobre o terminal integrado no Studio de operações do SQL (visualização).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 0754c66c182acefd2fdff799b791fbf135356d7b
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34234711"
---
# <a name="integrated-terminal"></a>Terminal integrado

Em [!INCLUDE[name-sos](../includes/name-sos-short.md)], você pode abrir um terminal integrado, inicialmente, iniciando na raiz do seu espaço de trabalho. Isso pode ser conveniente, pois não é necessário alternar windows ou alterar o estado de um terminal existente para executar uma tarefa de linha de comando rápida.

Para abrir o terminal:

* Use o **Ctrl +'** atalho de teclado com o caractere de acento grave.
* Use o **exibição** | **Terminal integrada** comando de menu.
* Do **comando paleta** (**Ctrl + Shift + P**), use o **Terminal integrado de alternância de exibição:** comando.

![Terminal](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Você ainda pode abrir um shell externo com o Gerenciador de **abrir no Prompt de comando** comando (**abrir no Terminal** no Mac ou Linux) se você preferir trabalhar fora [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="managing-multiple-terminals"></a>Gerenciando vários terminais

Você pode criar vários terminais aberta para diferentes locais e navegar facilmente entre eles. Instâncias de terminal podem ser adicionadas ao atingir o ícone mais na parte superior direita do **TERMINAL** painel ou por disparar o **Ctrl + Shift +'** comando. Isso cria outra entrada na lista suspensa que pode ser usada para alternar entre eles.

![Vários terminais](media/integrated-terminal/terminal-multiple-instances.png)

Remover instâncias de terminal, pressionando a Lixeira podem botão.

> [!TIP]
> Se você usar vários terminais extensivamente, você pode adicionar associações de chave para o `focusNext`, `focusPrevious` e `kill` comandos descritos no [seção associações de chave](#key-bindings) para permitir a navegação entre eles usando apenas o teclado.

## <a name="configuration"></a>Configuração

O shell usado o padrão é `$SHELL` em Linux e macOS, PowerShell no Windows 10 e o cmd.exe em versões anteriores do Windows. Esses podem ser substituídas manualmente pela configuração `terminal.integrated.shell.*` na [configurações](settings.md). Argumentos podem ser passados para o shell de terminal no Linux e macOS usando o `terminal.integrated.shellArgs.*` configurações.

### <a name="windows"></a>Windows

Configurar corretamente o shell no Windows é uma questão de localizar o executável correto e atualizando a configuração. Abaixo está uma lista de arquivos executáveis do shell comuns e seus locais padrão:

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
> Para ser usado como um terminal integrado, o executável de shell deve ser um aplicativo de console para que `stdin/stdout/stderr` podem ser redirecionados.

> [!TIP]
> O shell integrado de terminal está sendo executado com as permissões de [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Se você precisa executar um shell de comando com privilégios elevados (administrador) ou permissões diferentes, você pode usar os utilitários de plataforma como `runas.exe` dentro de um terminal.

### <a name="shell-arguments"></a>Argumentos de shell

Você pode passar argumentos para o shell quando ele é iniciado.

Por exemplo, para habilitar bash em execução como um shell de logon (qual é executado `.bash_profile`), passar o `-l` argumento (com aspas duplas):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>Configurações de exibição de terminal

Você pode personalizar a fonte de terminal integrada e a altura da linha com as seguintes configurações:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>Associações de chave de terminal

O **exibição: alternância integrado Terminal** comando está associado a **Ctrl +'** para alternar rapidamente o painel de terminal integrado e sair do modo de exibição.

Abaixo estão os atalhos de teclado para navegar rapidamente no terminal integrado:

Chave|Comando
---|---
**CTRL +'**|Mostrar terminal integrado
**Ctrl + Shift +'**|Criar novo terminal
**CTRL + seta para cima**|Role para cima
**CTRL + seta para baixo**|Role para baixo
**Ctrl + PageUp**|Página de rolagem para cima
**Ctrl + PageDown**|Página de rolagem para baixo
**CTRL + Home**|Role para cima
**CTRL + End**|Role para baixo
**CTRL + K**|Limpar o terminal

Outros comandos de terminal estão disponíveis e podem ser vinculados a seus atalhos de teclado preferencial.

São eles:

* `workbench.action.terminal.focus`: O terminal o foco. Isso é como alternar mas concentra-se o terminal em vez de ocultá-lo, se ele estiver visível.
* `workbench.action.terminal.focusNext`: Concentra-se a próxima instância de terminal.
* `workbench.action.terminal.focusPrevious`: Concentra-se a instância anterior de terminal.
* `workbench.action.terminal.kill`: Remova a instância atual de terminal.
* `workbench.action.terminal.runSelectedText`: Execute o texto selecionado na instância de terminal.
* `workbench.action.terminal.runActiveFile`: Execute o arquivo de ativo na instância de terminal.

### <a name="run-selected-text"></a>Executar o texto selecionado

Para usar o `runSelectedText` de comando, selecione o texto em um editor e execute o comando **Terminal: executar texto selecionado no Terminal Active** via o **comando paleta** (**Ctrl + Shift + P**). O terminal tenta executar o texto selecionado:

![Executar o texto selecionado](media/integrated-terminal/terminal_run_selected.png)

Se nenhum texto selecionado no editor ativo, a linha que o cursor está sobre é executada no terminal.

### <a name="copy--paste"></a>Copiar e colar

Os atalhos para copiar e colar sigam os padrões de plataforma:

* Linux: **Ctrl + Shift + C** e **Ctrl + Shift + V**
* Mac: **Cmd + C** e **Cmd + V**
* Windows: **Ctrl + C** e **Ctrl + V**

### <a name="find"></a>Localizar

O Terminal integrada oferece a funcionalidade de localização básica que pode ser disparada com **Ctrl + F**.

Se você quiser **Ctrl + F** para ir para o shell em vez de iniciar o widget de localização em Linux e Windows, você precisa remover o keybinding da seguinte forma:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>Renomear as sessões de terminal

Sessões de Terminal integradas agora podem ser renomeadas usando o **Terminal: Renomear** (`workbench.action.terminal.rename`) comando. O novo nome é exibido na lista suspensa de seleção terminal.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>Forçar as associações de chave para passar o terminal

Enquanto o foco estiver no terminal integrado, muitos associações de chave não funcionarão porque os pressionamentos de teclas são passados para e consumidos pelo terminal em si. O `terminal.integrated.commandsToSkipShell` configuração pode ser usada para contornar esse problema. Ele contém uma matriz de nomes de comando cujas associações de chave ignorar o processamento pelo shell e em vez disso, ser processadas pelo [!INCLUDE[name-sos](../includes/name-sos-short.md)] sistema de associação de chave. Por padrão, isso inclui todas as associações de chave terminal além de uma associação chave usadas de alguns select.

