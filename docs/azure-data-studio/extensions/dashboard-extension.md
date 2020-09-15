---
title: Criar uma extensão de painel
description: Este tutorial demonstra como criar uma extensão de painel para adicionar uma funcionalidade personalizada ao Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.reviewer: alayu, maghan
ms.topic: how-to
author: yualan
ms.author: alayu
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: b28b3cd043d6564da7d644bb44469671c9ffa147
ms.sourcegitcommit: c5f0c59150c93575bb2bd6f1715b42716001126b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89392135"
---
# <a name="create-an-azure-data-studio-dashboard-extension"></a>Criar uma extensão de painel do Azure Data Studio

Este tutorial demonstra como criar uma **extensão de painel do Azure Data Studio**. A extensão contribui para o painel de conexão do Azure Data Studio, de modo que você possa estender a funcionalidade do Azure Data Studio de maneira que seja facilmente visível para os usuários.

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> - Instalar o gerador de extensão
> - Criar sua extensão
> - Contribuir para o painel na extensão
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

## <a name="create-your-dashboard-extension"></a>Criar a extensão de painel

### <a name="introduction-to-the-dashboard"></a>Introdução ao painel

O painel de conexão do Azure Data Studio é uma ferramenta avançada que resume e fornece insights sobre as conexões de um usuário.

Há duas variações do painel: o 'painel de servidor' que resume todo o servidor e o 'painel de banco de dados' que resume um banco de dados individual. Acesse-o clicando com o botão direito do mouse em um servidor ou um banco de dados na visualização Conexões do Azure Data Studio e clicando em **Gerenciar**:

:::image type="content" source="media/dashboard-extension/dashboard-summary.gif" alt-text="Introdução aos painéis":::

Há três pontos de contribuição principais para que as extensões adicionem uma funcionalidade ao painel:

1. **Guia de Painel Completo**: uma guia separada no painel para a extensão. Pode ser adicionada a um painel de banco de dados ou de servidor. Personalizável com widgets, uma barra de ferramentas e uma seção de navegação.
2. **Ações da Home Page**: botões de ação na parte superior da barra de ferramentas de conexão.
3. **Widgets**: grafos que são executados no SQL Server.

:::image type="content" source="media/dashboard-extension/dashboard-contrib-points.png" alt-text="Pontos de contribuição":::

### <a name="run-the-extension-generator"></a>Executar o gerador de extensão

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo azuredatastudio`

2. Escolha **Novo Dashboard** na lista de tipos de extensão.

3. Preencha os avisos, conforme mostrado abaixo. Isso criará uma extensão que contribui com uma guia para o Painel de Servidor.

:::image type="content" source="media/dashboard-extension/dashboard-generator.png" alt-text="Gerador de extensão":::

Como há muitos avisos, veja um pouco mais de informações sobre o que cada pergunta significa:

:::image type="content" source="media/dashboard-extension/dashboard-flowchart.png" alt-text="Fluxograma de painéis":::

Seguir as etapas anteriores cria uma nova pasta. Abra a pasta no Visual Studio Code e você estará pronto para criar sua extensão de painel.

### <a name="run-the-extension"></a>Executar a extensão

Vamos ver o que o modelo de painel nos oferece executando a extensão. Antes da execução, verifique se a **extensão de Depuração do Azure Data Studio** está instalada no Visual Studio Code.

Selecione **F5** no VS Code para iniciar o Azure Data Studio no modo de depuração com a extensão em execução. Em seguida, você poderá ver como esse modelo padrão contribui para o painel.

Depois, veremos como modificar esse painel padrão.

### <a name="develop-the-dashboard"></a>Desenvolver o painel

O arquivo mais importante para começar a usar o desenvolvimento de extensões é `package.json`. Esse é o arquivo de manifesto, no qual as contribuições do painel são registradas. Observe as seções `dashboard.tabs`, `dashboard.insights`e `dashboard.containers`.

Estas são algumas alterações para você experimentar:

- Explore os tipos de insights, incluindo 'bar', 'horizontalBar' e 'timeSeries'
- Escreva suas consultas para executá-la na conexão do SQL Server
- Veja este [tutorial de insight de exemplo](../tutorial-qds-sql-server.md) ou [este](../tutorial-table-space-sql-server.md) para obter tutoriais de insights específicos

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar com outras pessoas, você precisa empacotar a extensão em um único arquivo. Ele pode ser publicado no marketplace de extensões do Azure Data Studio ou compartilhado entre sua equipe ou comunidade. Para fazer isso, você precisa instalar outro pacote npm na linha de comando:

```console
`npm install -g vsce`
```

Edite o `README.md` como desejar, procure o diretório base da extensão e execute `vsce package`. Opcionalmente, você pode vincular um repositório com a extensão ou continuar sem um. Para adicionar um, adicione uma linha semelhante ao arquivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

Depois que essas linhas forem adicionadas, um arquivo my-test-extension-0.0.1.vsix terá sido criado e estará pronto para ser instalado no Azure Data Studio.

:::image type="content" source="media/dashboard-extension/install-vsix.png" alt-text="Instalar o VSIX":::

## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no marketplace

O marketplace de extensões do Azure Data Studio ainda não está totalmente implementado, mas o processo atual é hospedar o VSIX da extensão em algum lugar (por exemplo, uma página de Versão do GitHub) e enviar uma PR atualizando [este arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com as informações de sua extensão.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> - Instalar o gerador de extensão
> - Criar sua extensão
> - Contribuir para o painel na extensão
> - Testar sua extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

Esperamos que, depois de ler isto, você se sinta inspirado a criar sua própria extensão para o Azure Data Studio. Temos suporte para Insights do Painel (grafos bonitos que são executados em seu SQL Server), várias APIs específicas do SQL e um grande conjunto de pontos de extensão herdados do Visual Studio Code.

Se você tiver uma ideia, mas não souber exatamente como começar, abra um problema ou envie um tweet para a equipe: [azuredatastudio](https://twitter.com/azuredatastudio).

Você sempre pode consultar o [Guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview), pois ele abrange todas as APIs e padrões existentes.

Para saber como trabalhar com T-SQL no Azure Data Studio, conclua o tutorial do Editor de T-SQL:

> [!div class="nextstepaction"]
> [Usar o editor de Transact-SQL para criar objetos de banco de dados](../tutorial-sql-editor.md).
