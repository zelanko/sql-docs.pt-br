---
title: Notebooks com o kernel do Kusto no Azure Data Studio
description: Este tutorial mostra como criar e executar um notebook do Kusto.
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: a8379e10e8c3e3af64381e9a4536b253e203964e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725120"
---
# <a name="create-and-run-a-kusto-kql-notebook-preview"></a>Criar e executar um notebook do Kusto (KQL) (versão prévia)

Este artigo mostra como criar e executar um [notebook do Azure Data Studio](./notebooks-guidance.md) usando a [extensão do Kusto (KQL)](../extensions/kusto-extension.md), conectando-se a um cluster do Azure Data Explorer.

Com a extensão do Kusto (KQL), você pode alterar a opção de kernel para **Kusto**.

Esse recurso está atualmente na visualização.

## <a name="prerequisites"></a>Pré-requisitos

Caso você não tenha uma assinatura do Azure, crie uma [conta gratuita do Azure](https://azure.microsoft.com/free/) antes de começar.

- [Um cluster do Azure Data Explorer com um banco de dados ao qual você pode se conectar](/azure/data-explorer/create-cluster-database-portal).
- [Azure Data Studio](../download-azure-data-studio.md).
- [Extensão do Kusto (KQL) para o Azure Data Studio](../extensions/kusto-extension.md).

## <a name="create-a-kusto-kql-notebook"></a>Criar um notebook do Kusto (KQL)

As seguintes etapas mostram como criar um arquivo de notebook no Azure Data Studio:

1. No Azure Data Studio, conecte-se ao cluster do Azure Data Explorer.

2. Navegue até o painel **Conexões** e, na janela **Servidores**, clique com o botão direito do mouse no banco de dados do Kusto e selecione *Novo Notebook*. Você também pode ir para **Arquivo** > **Novo Notebook**.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-new-notebook.png" alt-text="Abrir notebook":::

3. Selecione *Kusto* para o **Kernel**. Verifique se o menu **Anexar** está definido para o nome do cluster e o banco de dados. Para este artigo, usamos o cluster help.kusto.windows.net com os dados do banco de dados Exemplos.

   :::image type="content" source="media/notebooks-kusto-kernel/set-kusto-kernel.png" alt-text="Abrir notebook":::

Você pode salvar o notebook usando o comando **Salvar** ou **Salvar como...** no menu **Arquivo**.

Para abrir um notebook, você pode usar o comando **Abrir arquivo...** no menu **Arquivo**, selecionar **Abrir arquivo** na página **Inicial** ou usar o comando **Arquivo: abrir** da paleta de comandos.

## <a name="change-the-connection"></a>Alterar a conexão

Para alterar a conexão de um notebook ao Kusto:

1. Selecione o menu **Anexar a** na barra de ferramentas do notebook e, em seguida, **Alterar Conexão**.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-select-attach-to-change-connections.png" alt-text="Abrir notebook":::

   > [!Note]
   > Verifique se o valor do banco de dados é populado. Os notebooks do Kusto precisam ter o banco de dados especificado.

2. Agora você pode selecionar um servidor de conexão recente ou inserir novos detalhes de conexão para se conectar.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-change-connection-cluster.png" alt-text="Abrir notebook":::

   > [!Note]
   > Especifique o nome do cluster sem o `https://`.

## <a name="run-a-code-cell"></a>Executar uma célula de código

Você pode criar células contendo consultas KQL que podem ser executadas no local selecionando o botão **Executar célula** à esquerda da célula. Os resultados são mostrados no notebook após a execução da célula.

Por exemplo:

1. Adicione uma nova célula de código selecionando o comando **+Code** na barra de ferramentas.

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-kernel-code.png" alt-text="Abrir notebook":::

2. Copie e cole o exemplo a seguir na célula e selecione **Executar célula**. Este exemplo consulta os dados de StormEvents para um tipo de evento específico.

   ```kusto
    StormEvents
    | where EventType == "Waterspout"
   ```

   :::image type="content" source="media/notebooks-kusto-kernel/run-kusto-notebook-cell.png" alt-text="Abrir notebook":::

## <a name="save-the-result-or-show-chart"></a>Salvar o resultado ou mostrar o gráfico

Se você executar um script que retorna um resultado, poderá salvar esse resultado em formatos diferentes usando a barra de ferramentas exibida acima do resultado.

- Salvar como CSV
- Salvar como Excel
- Salvar como JSON
- Salvar como XML
- Mostrar Gráfico

```kusto
    StormEvents
    | limit 10
```

:::image type="content" source="media/notebooks-kusto-kernel/run-notebook-save-results.png" alt-text="Abrir notebook":::

## <a name="known-issues"></a>Problemas conhecidos

| Detalhes | Solução alternativa |
|---------|------------|
| [O resultado da consulta só mostra cabeçalhos de coluna](https://github.com/microsoft/azuredatastudio/issues/12565). | N/D |

Você pode arquivar uma [solicitação de recurso](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=) para fornecer comentários à equipe do produto.  
Você pode arquivar um [bug](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=) para fornecer comentários à equipe do produto.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks:

- [Extensão do Kusto (KQL) para o Azure Data Studio](../extensions/kusto-extension.md)
- [Como usar notebooks no Azure Data Studio](./notebooks-guidance.md)
- [Criar e executar um notebook do Python](./notebooks-python-kernel.md)
- [Criar e executar um notebook do SQL Server](./notebooks-sql-kernel.md)