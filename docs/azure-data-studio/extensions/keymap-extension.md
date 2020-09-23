---
title: Criar uma extensão de mapa de teclas
description: Este tutorial demonstra como criar uma extensão de mapa de teclas para adicionar uma funcionalidade personalizada ao Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: b1e1b5fb4d21e153133e76ff612f54c8153e0772
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111665"
---
# <a name="create-an-azure-data-studio-keymap-extension"></a>Criar uma extensão de mapa de teclas do Azure Data Studio

Este tutorial demonstra como criar uma nova extensão do Azure Data Studio. A extensão cria associações de teclas SSMS familiares no Azure Data Studio.

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> - Criar um projeto de extensão
> - Instalar o gerador de extensão
> - Criar sua extensão
> - Adicionar associações de teclas personalizadas à extensão
> - Testar sua extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

## <a name="prerequisites"></a>Pré-requisitos

O Azure Data Studio se baseia na mesma estrutura que o Visual Studio Code, portanto, as extensões para o Azure Data Studio são criadas usando o Visual Studio Code. Para começar, você precisa dos seguintes componentes:

- O [Node.js](https://nodejs.org) instalado e disponível em seu `$PATH`. O Node.js inclui o [npm](https://www.npmjs.com/), o Gerenciador de Pacotes do Node.js, que é usado para instalar o gerador de extensão.
- O [Visual Studio Code](https://code.visualstudio.com) para depurar a extensão.
- A [Extensão de depuração](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) do Azure Data Studio (opcional). Ela permite testar sua extensão sem a necessidade de empacotar e instalá-la no Azure Data Studio.
- Certifique-se de que `azuredatastudio` está em seu caminho. Para o Windows, escolha a opção `Add to Path` em setup.exe. Para Mac ou Linux, execute o *Comando instalar 'azuredatastudio' no caminho*.

## <a name="install-the-extension-generator"></a>Instalar o gerador de extensão

Para simplificar o processo de criação de extensões, criamos um [gerador de extensão](https://code.visualstudio.com/docs/extensions/yocode) usando o Yeoman. Para instalá-lo, execute o seguinte no prompt de comando:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-keymap-extension"></a>Criar a extensão de mapa de teclas

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo azuredatastudio`

2. Escolha **Novo Mapa de Chaves** na lista de tipos de extensão:

   :::image type="content" source="media/keymap-extension/extension-generator.png" alt-text="Gerador de extensão":::

3. Siga as etapas para preencher o nome da extensão (para este tutorial, use **ssmskeymap2**) e adicione uma descrição.

Seguir as etapas anteriores cria uma nova pasta. Abra a pasta no Visual Studio Code e você está pronto para criar sua própria extensão de associação de teclas!

### <a name="add-a-keyboard-shortcut"></a>Adicionar atalho de teclado

**Etapa 1: Localizar os atalhos a serem substituídos**

Agora que temos nossa extensão pronta para ser usada, adicione alguns atalhos de teclado SSMS (ou associações de teclas) ao Azure Data Studio. Eu usei a [Folha de referências de Andy Mallon](https://am2.co/2018/02/updated-cheat-sheet/) e a lista de atalhos de teclado da RedGate como inspiração.

Os itens de que mais senti falta foram:

- Executar uma consulta com o plano de execução real habilitado. Este é o comando **CTRL + M** no SSMS e não tem uma associação no Azure Data Studio.
- Ter **Ctrl + Shift + E** como uma segunda maneira de executar uma consulta. Os comentários dos usuários indicaram que isso estava faltando.
- Usar **ALT + F1** para executar `sp_help`. Adicionamos isso no Azure Data Studio, mas como essa associação já estava em uso, nós a mapeamos para **ALT+F2**.
- Alternar tela inteira (**SHIFT + ALT + ENTER**).
- **F8** para mostrar a exibição **Pesquisador de Objetos** / **Servidores**.

É fácil localizar e substituir essas associações de teclas. Execute *Abrir Atalhos de Teclado* para mostrar a guia **Atalhos de Teclado** no Azure Data Studio, pesquise por *consultar* e escolha **Alterar Associação de teclas**. Quando terminar de alterar a associação de teclas, você poderá ver o mapeamento atualizado no arquivo keybindings.json (execute *Abrir Atalhos de Teclado* para vê-lo).

:::image type="content" source="media/keymap-extension/keyboard-shortcuts.png" alt-text="Atalhos do teclado":::

:::image type="content" source="media/keymap-extension/key-bindings-json.png" alt-text="Extensão keybindings.json":::

**Etapa 2: Adicionar atalhos à extensão**

Para adicionar atalhos à extensão, abra o arquivo *package.json* (na extensão) e substitua a seção `contributes` pelo seguinte:

```json
"contributes": {
  "keybindings": [
    {
      "key": "shift+cmd+e",
      "command": "runQueryKeyboardAction"
    },
    {
      "key": "ctrl+cmd+e",
      "command": "workbench.view.explorer"
    },
    {
      "key": "alt+f1",
      "command": "workbench.action.query.shortcut1"
    },
    {
      "key": "shift+alt+enter",
      "command": "workbench.action.toggleFullScreen"
    },
    {
      "key": "f8",
      "command": "workbench.view.connections"
    },
    {
      "key": "ctrl+m",
      "command": "runCurrentQueryWithActualPlanKeyboardAction"
    }
  ]
}
```

## <a name="test-your-extension"></a>Testar sua extensão

Certifique-se de que `azuredatastudio` está em seu caminho executando o comando Instalar azuredatastudio no caminho no Azure Data Studio.

Certifique-se de que a extensão de Depuração do Azure Data Studio esteja instalada no Visual Studio Code.

Selecione **F5** para iniciar o Azure Data Studio no modo de depuração com a extensão em execução:

:::image type="content" source="media/keymap-extension/install-extension.png" alt-text="Instalar a extensão":::

:::image type="content" source="media/keymap-extension/test-extension.png" alt-text="testar extensão":::

Mapas de teclas são uma das extensões mais rápidas de serem criadas, portanto, sua nova extensão deve estar funcionando com êxito e pronta para ser compartilhada.

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar com outras pessoas, você precisa empacotar a extensão em um único arquivo. Ele pode ser publicado no marketplace de extensões do Azure Data Studio ou compartilhado entre sua equipe ou comunidade. Para fazer isso, você precisa instalar outro pacote npm na linha de comando:

```console
`npm install -g vsce`
```

Navegue até o diretório base da extensão e execute `vsce package`. Eu precisei adicionar duas linhas extras para impedir que a ferramenta *vsce* criasse problemas:

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

Depois disso, meu arquivo ssmskeymap-0.1.0.vsix foi criado e está pronto para ser instalado e compartilhado com o mundo!

:::image type="content" source="media/keymap-extension/extensions.png" alt-text="Instalar":::

## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no marketplace

O marketplace de extensões do Azure Data Studio ainda não está totalmente implementado, mas o processo atual é hospedar o VSIX da extensão em algum lugar (por exemplo, uma página de Versão do GitHub) e enviar uma PR atualizando [este arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com as informações de sua extensão.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> - Criar um projeto de extensão
> - Instalar o gerador de extensão
> - Criar sua extensão
> - Adicionar associações de teclas personalizadas à extensão
> - Testar sua extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

Esperamos que, depois de ler isto, você se sinta inspirado a criar sua própria extensão para o Azure Data Studio. Temos suporte para Insights do Painel (grafos bonitos que são executados em seu SQL Server), várias APIs específicas do SQL e um grande conjunto de pontos de extensão herdados do Visual Studio Code.

Se você tiver uma ideia, mas não souber exatamente como começar, abra um problema ou envie um tweet para a equipe: [azuredatastudio](https://twitter.com/azuredatastudio).

Você sempre pode consultar o [Guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview), pois ele abrange todas as APIs e padrões existentes.

Para saber como trabalhar com T-SQL no Azure Data Studio, conclua o tutorial do Editor de T-SQL:

> [!div class="nextstepaction"]
> [Usar o editor de Transact-SQL para criar objetos de banco de dados](../tutorial-sql-editor.md)
