---
title: 'Tutorial: Criar uma extensão'
titleSuffix: Azure Data Studio
description: Este tutorial demonstra como criar uma extensão para adicionar funcionalidade personalizada ao estúdio de dados do Azure.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: kevcunnane
ms.author: kcunnane
manager: craigg
ms.openlocfilehash: 0a4e877a91cad978bb62747bd50e40adaa69ef1c
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030600"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>Tutorial: Criar uma extensão do estúdio de dados do Azure

Este tutorial demonstra como criar uma nova extensão do estúdio de dados do Azure. A extensão cria as associações de teclas familiares do SSMS no estúdio de dados do Azure.

Durante este tutorial, você aprenderá como:
> [!div class="checklist"]
> * Criar um projeto de extensão
> * Instalar o gerador de extensão
> * Criar sua extensão
> * Testar sua extensão
> * Empacotar sua extensão
> * Publicar sua extensão no marketplace

## <a name="prerequisites"></a>Prerequisites

O estúdio de dados do Azure baseia-se na mesma estrutura como o Visual Studio Code, para que as extensões para o Studio de dados do Azure são criadas usando o Visual Studio Code. Para começar, você precisa dos seguintes componentes:

- [Node. js](https://nodejs.org) instalado e disponível no seu `$PATH`. Inclui o Node. js [npm](https://www.npmjs.com/), o Gerenciador de pacotes do Node. js, que é usado para instalar o gerador de extensão.
- [Visual Studio Code](https://code.visualstudio.com) para depurar a extensão.
- O estúdio de dados do Azure [extensão de depuração](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug).
- Certifique-se de `sqlops` está em seu caminho. Para Windows, verifique se você escolher o `Add to Path` opção no setup.exe. Para Mac ou Linux, execute as *instalar o comando 'sqlops' no caminho* opção.
- SQL Operations Studio depurar extensão (opcional). Isso lhe permite testar sua extensão sem a necessidade de empacotar e instalá-lo no estúdio de dados do Azure.


## <a name="install-the-extension-generator"></a>Instalar o gerador de extensão

Para simplificar o processo de criação de extensões, nós criamos uma [gerador de extensão](https://code.visualstudio.com/docs/extensions/yocode) usando o Yeoman. Para instalá-lo, execute o seguinte no prompt de comando:

`npm install -g yo generator-sqlops`

## <a name="create-your-extension"></a>Criar sua extensão

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo sqlops`

2. Escolher **novo mapa de teclas** na lista de tipos de extensão:

   ![Gerador de extensão](./media/tutorial-create-extension/extension-generator.png)

3. Siga as etapas para preencher o nome da extensão (para este tutorial, use **ssmskeymap**) e adicione uma descrição.

Concluir as etapas anteriores cria uma nova pasta. Abra a pasta no Visual Studio Code e você está pronto para criar sua própria extensão de associação de chave!


### <a name="add-a-keyboard-shortcut"></a>Adicionar um atalho de teclado

**Etapa 1: Localizar os atalhos para substituir**

Agora que temos nossa extensão pronto para começar, adicione alguns SSMS teclado atalhos (ou associações de teclas) no estúdio de dados do Azure. Eu usei [roteiro de Andy Mallon](https://am2.co/2018/02/updated-cheat-sheet/) e lista de atalhos de teclado da RedGate para se inspirar.

As principais coisas que eu vi ausentes foram:

- Execute uma consulta com o plano de execução real habilitado. Isso é **Ctrl + M** no SSMS e não tem uma associação no estúdio de dados do Azure.
- Tendo **CTRL + SHIFT + E** como uma segunda maneira de executar uma consulta. Comentários do usuário indicam que isso estava ausente.
- Tendo **ALT + F1** executar `sp_help`. Adicionamos isso no estúdio de dados do Azure, mas desde que a associação já estava em uso, é mapeado para **ALT + F2** em vez disso.
- Alternar tela inteira (**SHIFT + ALT + ENTER**).
- **F8** para mostrar **Pesquisador de objetos** / **modo de exibição servidores**.

É fácil de localizar e substituir essas associações de tecla. Executar *aberto atalhos de teclado* para mostrar a **atalhos de teclado** guia no estúdio de dados do Azure, procure *consulta* e, em seguida, escolha **deassociaçãodechavedealteração**. Quando você terminar alterando a associação de teclas, você pode ver o mapeamento atualizado no arquivo de KeyBindings. JSON (execute *atalhos de teclado aberto* para vê-lo).

![atalhos de teclado](./media/tutorial-create-extension/keyboard-shortcuts.png)

![extensão de KeyBindings. JSON](./media/tutorial-create-extension/keybindings-json.png)


**Etapa 2: Adicionar atalhos para a extensão**

Para adicionar atalhos para a extensão, abra o *Package. JSON* arquivo (extensão) e substitua o `contributes` seção com o seguinte:

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

Certifique-se de `azuredatastudio` está em seu caminho, executando o comando de instalação azuredatastudio no comando de caminho no estúdio de dados do Azure.

Certifique-se de que a extensão de depuração do Azure Data Studio está instalada no Visual Studio Code.

Selecione **F5** para iniciar o estúdio de dados do Azure no modo de depuração com a extensão em execução:

![Instalar extensão](./media/tutorial-create-extension/install-extension.png)

![extensão de teste](./media/tutorial-create-extension/test-extension.png)

Mapas de chave são uma das extensões mais rápidas para criar, portanto, sua nova extensão agora deve estar funcionando e pronto para compartilhar com êxito.

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar com outras pessoas, você precisará empacotar a extensão em um único arquivo. Isso pode ser publicado no marketplace de extensão do estúdio de dados do Azure ou compartilhado entre sua equipe ou da comunidade. Para fazer isso, você precisará instalar outro pacote npm da linha de comando:

`npm install -g vsce`

Navegue até o diretório base da extensão e executar `vsce package`. Tive de adicionar duas linhas extras para parar o *vsce* ferramenta do reclamando:

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

Depois que isso foi feito, o meu arquivo ssmskeymap 0.1.0.vsix foi criado e estará pronto para instalar e compartilhar com o mundo!

![Instalar extensão](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no marketplace

O marketplace de extensões do estúdio de dados do Azure ainda não está totalmente implementado, mas o processo atual é hospedar a extensão do VSIX em algum lugar (por exemplo, uma página de versão do GitHub), em seguida, enviar uma atualização de PR [esse arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com seu informações de extensão.


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Criar um projeto de extensão
> * Instalar o gerador de extensão
> * Criar sua extensão
> * Testar sua extensão
> * Empacotar sua extensão
> * Publicar sua extensão no marketplace


Esperamos que depois de ler isso, que você será inspirado para criar sua própria extensão para o estúdio de dados do Azure. Temos suporte para Insights de painel (bonitas gráficos que executam o SQL Server), uma série de APIs específicas do SQL e um enorme conjunto existente de pontos de extensão herdadas do Visual Studio Code.

Se você tem uma ideia, mas não estiver certo de como começar, abra um problema ou uma tweet com a equipe: [azuredatastudio](https://twitter.com/azuredatastudio).

Você sempre poderá consultar a [guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) porque ele aborda todos os padrões e APIs existentes.


Para saber como trabalhar com o T-SQL no estúdio de dados do Azure, conclua o tutorial do Editor T-SQL:

> [!div class="nextstepaction"]
> [Usar o editor Transact-SQL para criar objetos de banco de dados](tutorial-sql-editor.md).
