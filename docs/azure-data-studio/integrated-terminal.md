---
title: Terminal integrado
description: Saiba como abrir um terminal integrado ao Azure Data Studio. Um terminal integrado pode ser mais conveniente do que um separado.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 09876b320e4761e6d73756d9cf7db5fc6c66a0b6
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91363993"
---
# <a name="integrated-terminal"></a>Terminal Integrado

No Azure Data Studio, você pode abrir um terminal integrado inicialmente começando na raiz de seu workspace. Isso pode ser conveniente, pois você não precisa alternar janelas nem alterar o estado de um terminal existente para executar uma tarefa de linha de comando rápida.

Para abrir o terminal:

* Use o atalho de teclado **Ctrl + '** com o caractere de acento grave.
* Use o comando de menu **Exibir** | **Terminal Integrado**.
* Na **Paleta de Comandos** (**Ctrl+Shift+P**), use o comando **Exibir: Alternar Terminal Integrado**.

![Terminal](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Você ainda poderá abrir um shell externo com o comando do Explorer **Abrir no prompt de comando** (**Abrir no Terminal** no Mac ou no Linux) se preferir trabalhar fora do Azure Data Studio.

## <a name="managing-multiple-terminals"></a>Como gerenciar vários terminais

Você pode criar vários terminais abertos em locais diferentes e navegar facilmente entre eles. As instâncias de terminal podem ser adicionadas pressionando o ícone de adição na parte superior direita do painel **TERMINAL** ou disparando o comando **CTRL+ Shift+'** . Isso cria outra entrada na lista suspensa que pode ser usada para alternar entre elas.

![Vários terminais](media/integrated-terminal/terminal-multiple-instances.png)

Remova as instâncias de terminal pressionando o botão de lixeira.

> [!TIP]
> Se você usar vários terminais extensivamente, poderá adicionar associações de chave aos comandos `focusNext`, `focusPrevious` e `kill` descritos na seção [Associações de chave](#key-bindings) para permitir a navegação entre elas usando apenas o teclado.

## <a name="configuration"></a>Configuração

O shell usado usa como padrão `$SHELL` o Linux e o macOS, o PowerShell no Windows 10 e o cmd.exe em versões anteriores do Windows. Eles podem ser substituídos manualmente configurando `terminal.integrated.shell.*` em [configurações](settings.md). Os argumentos podem ser passados para o shell de terminal no Linux e no macOS usando as configurações `terminal.integrated.shellArgs.*`.

### <a name="windows"></a>Windows

Configurar corretamente o Shell no Windows é uma questão de localizar o executável correto e atualizar a configuração. Veja abaixo uma lista de executáveis comuns do Shell e seus locais padrão:

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
> Para ser usado como um terminal integrado, o executável do shell deve ser um aplicativo de console para que o `stdin/stdout/stderr` possa ser redirecionado.

> [!TIP]
> O shell de terminal integrado está sendo executado com as permissões do Azure Data Studio. Se você precisar executar um comando do shell com permissões elevadas (administrador) ou diferentes, poderá usar utilitários de plataforma como `runas.exe` em um terminal.

### <a name="shell-arguments"></a>Argumentos de Shell

Você pode passar argumentos para o shell quando ele é iniciado.

Por exemplo, para habilitar a execução do Bash como um shell de logon (que executa `.bash_profile`), passe o argumento `-l` (com aspas duplas):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>Configurações de exibição do terminal

Você pode personalizar a fonte de terminal integrado e a altura da linha com as seguintes configurações:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a name="terminal-key-bindings"></a><a id="key-bindings"></a>Associações de chave de terminal

O comando **Exibir: alternar Terminal Integrado** está associado a **CTRL+'** para alternar rapidamente o painel do terminal integrado para dentro e fora da exibição.

Abaixo estão os atalhos de teclado para navegar rapidamente dentro do terminal integrado:

|Chave|Comando|  
|---|---|  
|**Ctrl+\`**|Mostrar o terminal integrado|  
|**Ctrl+Shift+\`**|Criar novo terminal|  
|**Ctrl+Seta para cima**|Rolar para cima|  
|**Ctrl+Seta para baixo**|Rolar para baixo|  
|**Ctrl+PageUp**|Rolar página para cima|  
|**Ctrl+PageDown**|Rolar página para baixo|  
|**Ctrl+Home**|Rolar para o topo|  
|**Ctrl+End**|Rolar para a parte inferior|  
|**Ctrl+K**|Limpar o terminal|  

Outros comandos de terminal estão disponíveis e podem ser vinculados aos seus atalhos de teclado preferenciais.

Eles são:

* `workbench.action.terminal.focus`: focar o terminal. É como alternar, mas foca o terminal, em vez de ocultá-lo, se estiver visível.
* `workbench.action.terminal.focusNext`: focar a próxima instância de terminal.
* `workbench.action.terminal.focusPrevious`: focar a instância de terminal anterior.
* `workbench.action.terminal.kill`: remover a instância de terminal atual.
* `workbench.action.terminal.runSelectedText`: executar o texto selecionado na instância de terminal.
* `workbench.action.terminal.runActiveFile`: executar o arquivo ativo na instância de terminal.

### <a name="run-selected-text"></a>Executar o texto selecionado

Para usar o comando `runSelectedText`, selecione o texto em um editor e execute o comando **Terminal: executar o texto selecionado no terminal ativo** por meio da **Paleta de Comandos** (**Ctrl+Shift+P**). O terminal tenta executar o texto selecionado:

![Executar o texto selecionado](media/integrated-terminal/terminal_run_selected.png)

Se nenhum texto for selecionado no editor ativo, a linha em que o cursor está em execução será executada no terminal.

### <a name="copy--paste"></a>Copiar e colar

As associações de teclas para copiar e colar seguem os padrões de plataforma:

* Linux: **Ctrl+Shift+C** e **Ctrl+Shift+V**
* Mac: **Cmd+C** e **Cmd+V**
* Windows: **Ctrl+C** e **Ctrl+V**

### <a name="find"></a>Localizar

O terminal integrado tem a funcionalidade de localização básica que pode ser disparada com **Ctrl+F**.

Se você quiser que **CTRL+F** vá para o shell, em vez de iniciar o widget Find no Linux e no Windows, será necessário remover a associação de teclas da seguinte forma:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>Renomear sessões de terminal

As sessões do Terminal Integrado agora podem ser renomeadas usando o comando **Terminal: Renomear** (`workbench.action.terminal.rename`). O novo nome é exibido na lista suspensa da seleção de terminal.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>Como forçar associações de teclas a passarem pelo terminal

Embora o foco esteja no terminal integrado, muitas associações de teclas não funcionarão porque os pressionamentos de tecla são passados e consumidos pelo próprio terminal. A configuração `terminal.integrated.commandsToSkipShell` pode ser usada para contornar isso. Ela contém uma matriz de nomes de comando cujas associações de teclas ignoram o processamento pelo shell e, em vez disso, são processadas pelo sistema de associação de teclas do Azure Data Studio. Por padrão, isso inclui todas as associações de teclas de terminal, além de uma seleção de algumas associações de teclas usadas com frequência.

