---
title: Criar uma extensão de painel
description: Este tutorial demonstra como criar uma extensão de painel para adicionar uma funcionalidade personalizada ao Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 091bf94f01c66b3f991c0457adcfa4d119d49167
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364093"
---
# <a name="create-an-azure-data-studio-dashboard-extension"></a>Criar uma extensão de painel do Azure Data Studio

Este tutorial demonstra como criar uma extensão de painel do Azure Data Studio. A extensão contribui para o painel de conexão do Azure Data Studio, de modo que você possa estender a funcionalidade do Azure Data Studio de maneira que seja facilmente visível para os usuários.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> - Instalar o gerador de extensão.
> - Criar sua extensão.
> - Contribuir para o painel em sua extensão.
> - Testar sua extensão.
> - Empacotar sua extensão.
> - Publicar sua extensão no marketplace.

## <a name="prerequisites"></a>Pré-requisitos

O Azure Data Studio se baseia na mesma estrutura que o Visual Studio Code, portanto, as extensões para o Azure Data Studio são criadas usando o Visual Studio Code. Para começar, você precisa dos seguintes componentes:

- O [Node.js](https://nodejs.org) instalado e disponível em seu `$PATH`. O Node.js inclui o [npm](https://www.npmjs.com/), o Gerenciador de Pacotes do Node.js, que é usado para instalar o gerador de extensão.
- O [Visual Studio Code](https://code.visualstudio.com) para depurar a extensão.
- A [Extensão de depuração](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) do Azure Data Studio (opcional). A Extensão de depuração permite testar sua extensão sem a necessidade de empacotá-la e instalá-la no Azure Data Studio.
- Certifique-se de que `azuredatastudio` está em seu caminho. Para o Windows, escolha a opção **Adicionar ao Caminho** em setup.exe. Para Mac ou Linux, execute o **Comando instalar 'azuredatastudio' no caminho**.

## <a name="install-the-extension-generator"></a>Instalar o gerador de extensão

Para simplificar o processo de criação de extensões, criamos um [gerador de extensão](https://code.visualstudio.com/docs/extensions/yocode) usando o Yeoman. Para instalá-lo, execute o seguinte comando no prompt de comando:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-dashboard-extension"></a>Criar a extensão de painel

### <a name="introduction-to-the-dashboard"></a>Introdução ao painel

O painel de conexão do Azure Data Studio é uma ferramenta avançada que resume e fornece insights sobre as conexões de um usuário.

Há duas variações do painel. O *painel de servidor* resume todo o servidor e o *painel de banco de dados* resume um banco de dados individual. Acesse o painel clicando com o botão direito do mouse em um servidor ou um banco de dados no viewlet **Conexões** do Azure Data Studio e selecionando **Gerenciar**.

:::image type="content" source="media/dashboard-extension/dashboard-summary.gif" alt-text="Captura de tela que mostra a introdução dos painéis.":::

Há três pontos de contribuição principais para que as extensões adicionem uma funcionalidade ao painel:

1. **Guia de Painel Completo**: uma guia separada no painel para a extensão. Pode ser adicionada a um painel de banco de dados ou de servidor. Personalizável com widgets, uma barra de ferramentas e uma seção de navegação.
2. **Ações da Home Page**: botões de ação na parte superior da barra de ferramentas de conexão.
3. **Widgets**: grafos que são executados no SQL Server.

   :::image type="content" source="media/dashboard-extension/dashboard-contrib-points.png" alt-text="Captura de tela que mostra a introdução dos painéis.":::

### <a name="run-the-extension-generator"></a>Executar o gerador de extensão

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo azuredatastudio`

1. Escolha **Novo Dashboard** na lista de tipos de extensão.

1. Preencha os prompts, conforme mostrado, para criar uma extensão que contribui com uma guia para o painel de servidor.

   :::image type="content" source="media/dashboard-extension/dashboard-generator.png" alt-text="Captura de tela que mostra a introdução dos painéis.":::

   Como há muitos prompts, veja um pouco mais de informações sobre o que cada pergunta significa:

   :::image type="content" source="media/dashboard-extension/dashboard-flowchart.png" alt-text="Captura de tela que mostra a introdução dos painéis.":::

Seguir as etapas anteriores cria uma nova pasta. Abra a pasta no Visual Studio Code e você estará pronto para criar sua extensão de painel.

### <a name="run-the-extension"></a>Executar a extensão

Vamos ver o que o modelo de painel nos oferece executando a extensão. Antes de executá-la, verifique se a **extensão de Depuração do Azure Data Studio** está instalada no Visual Studio Code.

Selecione **F5** no Visual Studio Code para iniciar o Azure Data Studio no modo de depuração com a extensão em execução. Em seguida, você poderá ver como esse modelo padrão contribui para o painel.

Depois, veremos como modificar esse painel padrão.

### <a name="develop-the-dashboard"></a>Desenvolver o painel

O arquivo mais importante para começar a usar o desenvolvimento de extensões é `package.json`. Esse é o arquivo de manifesto, no qual as contribuições do painel são registradas. Observe as seções `dashboard.tabs`, `dashboard.insights`e `dashboard.containers`.

Estas são algumas alterações para você experimentar:

- Explore os tipos de insights, que incluem bar, horizontalBar e timeSeries.
- Escreva suas consultas para executá-las na conexão do SQL Server.
- Confira este [tutorial de insight de exemplo](../tutorial-qds-sql-server.md) ou [este tutorial](../tutorial-table-space-sql-server.md) para obter tutoriais de insights específicos.

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar a extensão com outras pessoas, você precisará empacotá-la em um só arquivo. Sua extensão pode ser publicada no marketplace de extensões do Azure Data Studio ou compartilhada entre a sua equipe ou sua comunidade. Para realizar essa etapa, você precisa instalar outro pacote npm da linha de comando.

```console
`npm install -g vsce`
```

Edite o arquivo `README.md` de sua preferência. Navegue até o diretório base da extensão e execute `vsce package`. Opcionalmente, você pode vincular um repositório com a extensão ou continuar sem um. Para adicionar um, adicione uma linha semelhante ao arquivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

Depois que essas linhas forem adicionadas, um arquivo `my-test-extension-0.0.1.vsix` será criado e estará pronto para ser instalado no Azure Data Studio.

:::image type="content" source="media/dashboard-extension/install-vsix.png" alt-text="Captura de tela que mostra a introdução dos painéis.":::

## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no marketplace

O marketplace de extensões do Azure Data Studio está em construção. O processo atual é hospedar o VSIX de extensão em algum lugar, por exemplo, em uma página de versão do GitHub. Em seguida, envie uma solicitação de pull que atualiza [esse arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com suas informações de extensão.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> - Instalar o gerador de extensão.
> - Criar sua extensão.
> - Contribuir para o painel em sua extensão.
> - Testar sua extensão.
> - Empacotar sua extensão.
> - Publicar sua extensão no marketplace.

Esperamos que, depois de ler esse artigo, você tenha inspiração para criar uma extensão para o Azure Data Studio. Temos suporte para Insights do Painel (grafos atraentes que são executados em seu SQL Server), várias APIs específicas do SQL e um grande conjunto de pontos de extensão herdados do Visual Studio Code.

Caso tenha uma ideia, mas não saiba exatamente como começar a desenvolvê-la, abra um problema ou envie um tweet para a equipe em [azuredatastudio](https://twitter.com/azuredatastudio).

Para obter mais informações, o [guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) abrange todas as APIs e os padrões existentes.

Para saber como trabalhar com T-SQL no Azure Data Studio, conclua o tutorial do Editor de T-SQL:

> [!div class="nextstepaction"]
> [Usar o editor de Transact-SQL para criar objetos de banco de dados](../tutorial-sql-editor.md)
