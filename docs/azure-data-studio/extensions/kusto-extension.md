---
title: Extensão do Kusto (KQL) para o Azure Data Studio
description: Este artigo descreve como você pode se conectar e consultar clusters do Azure Data Explorer com o Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 2ffe3945f8dd7e8c0ce9cf504c09622ca1a20331
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725185"
---
# <a name="kusto-kql-extension-for-azure-data-studio-preview"></a>Extensão do Kusto (KQL) para o Azure Data Studio (versão prévia)

A extensão do Kusto (KQL) para o [Azure Data Studio](../what-is.md) permite que você se conecte e consulte clusters do [Azure Data Explorer](/azure/data-explorer/data-explorer-overview).

Os usuários podem escrever e executar consultas do KQL e criar notebooks com o [kernel do Kusto](../notebooks/notebooks-kusto-kernel.md) completo com o IntelliSense.

Ao habilitar a experiência nativa do Kusto (KQL) no Azure Data Studio, os engenheiros de dados, os cientistas de dados e os analistas de dados podem observar rapidamente tendências e anomalias em grandes quantidades de dados armazenados no Azure Data Explorer.

Esta extensão está em versão prévia.

## <a name="prerequisites"></a>Pré-requisitos

Caso você não tenha uma assinatura do Azure, crie uma [conta gratuita do Azure](https://azure.microsoft.com/free/) antes de começar.

Os seguintes pré-requisitos também são necessários:

- [Azure Data Studio instalado](../download-azure-data-studio.md).
- [Um cluster e um banco de dados do Azure Data Explorer](/azure/data-explorer/create-cluster-database-portal).

## <a name="install-the-kusto-kql-extension"></a>Instalar a extensão do Kusto (KQL)

Para instalar a extensão do Kusto (KQL) no Azure Data Studio, siga as etapas abaixo.

1. Abra o gerenciador de extensões no Azure Data Studio. Você poderá selecionar o ícone de extensões ou selecionar **Extensões** no menu Exibir.

2. Digite *Kusto* na barra de pesquisa.

3. Selecione a extensão do **Kusto (KQL)** e veja os detalhes dessa extensão.

4. Selecione **Instalar**.

:::image type="content" source="media/kusto-extension/kusto-extension-icon.png" alt-text="Extensão do Kusto":::

## <a name="how-to-connect-to-an-azure-data-explorer-cluster"></a>Como se conectar a um cluster do Azure Data Explorer

### <a name="find-your-azure-data-explorer-cluster"></a>Localizar o cluster do Azure Data Explorer

Localize o cluster do Azure Data Explorer no [portal do Azure](https://ms.portal.azure.com/#home) e, em seguida, localize o URI para o cluster.

:::image type="content" source="media/kusto-extension/kusto-extension-adx-cluster-uri.png" alt-text="Extensão do Kusto":::

No entanto, você pode começar imediatamente usando o cluster *help.kusto.windows.net*.

Para este artigo, estamos usando dados do cluster help.kusto.windows.net para obter exemplos.

### <a name="connection-details"></a>Detalhes da conexão

Para configurar um cluster do Azure Data Explorer ao qual se conectar, siga as etapas abaixo.

1. Selecione **Nova conexão** no painel **Conexões**.

2. Preencha as informações em **Detalhes da Conexão**.
    1. Para **Tipo de conexão**, selecione *Kusto*.
    2. Para **Cluster**, insira o cluster do Azure Data Explorer.

        > [!Note]
        > Ao inserir o nome do cluster, não inclua o prefixo `https://` nem uma `/` à direita.

    3. Para **Tipo de Autenticação**, use o padrão – *Azure Active Directory – Universal com a conta de MFA*.
    4. Para **Conta**, use as informações da conta.
    5. Para **Banco de Dados**, use *Padrão*.
    6. Para **Grupo de Servidores**, use *Padrão*.
        1. É possível usar esse campo para organizar os servidores em um grupo específico.
    7. Deixe **Nome (opcional)** em branco.
        1. É possível usar esse campo para dar um alias ao seu servidor.

    :::image type="content" source="media/kusto-extension/kusto-extension-connection-details.png" alt-text="Extensão do Kusto":::

## <a name="how-to-query-an-azure-data-explorer-database-in-azure-data-studio"></a>Como consultar um banco de dados do Azure Data Explorer no Azure Data Studio

Agora que você configurou uma conexão com o cluster do Azure Data Explorer, pode consultar seus bancos de dados usando o Kusto (KQL).

Para criar uma guia de consulta, é possível selecionar **Arquivo > Nova Consulta**, usar *Ctrl + N* ou clicar com o botão direito do mouse no banco de dados e selecionar **Nova Consulta**.

Depois de abrir a nova guia de consulta, insira sua consulta do Kusto.

Aqui estão alguns exemplos de consultas do KQL:

```kusto
StormEvents
| limit 1000
```

```kusto
StormEvents
| where EventType == "Waterspout"
```

Para obter mais informações sobre como escrever consultas do KQL, visite [Escrever consultas para o Azure Data Explorer](/azure/data-explorer/write-queries#overview-of-the-query-language)

## <a name="view-extension-settings"></a>Exibir configurações da extensão

Para alterar as configurações da extensão do Kusto, siga as etapas abaixo.

1. Abra o gerenciador de extensões no Azure Data Studio. Você poderá selecionar o ícone de extensões ou selecionar **Extensões** no menu Exibir.

2. Localize a extensão do **Kusto (KQL)** .

3. Selecione o ícone **Gerenciar**.

4. Selecione o ícone **Configurações da Extensão**.

As configurações das extensões se parecem com esta:

:::image type="content" source="media/kusto-extension/kusto-extension-settings.png" alt-text="Extensão do Kusto":::

## <a name="sanddance-visualization"></a>Visualização do SandDance

A [extensão do SandDance](../sanddance-extension.md) com a extensão do Kusto (KQL) no Azure Data Studio reúne visualizações interativas avançadas. No conjunto de resultados da consulta do KQL, selecione o botão **Visualizador** para iniciar o [SandDance](https://sanddance.js.org/).

:::image type="content" source="media/kusto-extension/kusto-extension-sanddance-demo.gif" alt-text="Extensão do Kusto":::

## <a name="known-issues"></a>Problemas conhecidos

| Detalhes | Solução alternativa |
|---------|------------|
| [Após ser recarregado, o viewlet de conexão do Kusto não funciona](https://github.com/microsoft/azuredatastudio/issues/12475). | N/D |
| [Não é possível se reconectar automaticamente](https://github.com/microsoft/azuredatastudio/issues/11830). | Desconecte-se e reconecte-se ao cluster do Azure Data Explorer. |
| [A atualização do cluster do Kusto não parece se reconectar corretamente](https://github.com/microsoft/azuredatastudio/issues/11824). | Desconecte-se e reconecte-se ao cluster do Azure Data Explorer. |
| [A conexão com um cluster deve exibir o painel de cluster em vez de um banco de dados](https://github.com/microsoft/azuredatastudio/issues/12549) | N/D |
| Para cada tabela em seu banco de dados de cluster de dados do Azure, há apenas uma opção para **SELECIONAR AS 1000 MELHORES** em vez de **USAR 10**. | N/D |

Você pode arquivar uma [solicitação de recurso](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=) para fornecer comentários à equipe do produto.  
Você pode arquivar um [bug](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=) para fornecer comentários à equipe do produto.

## <a name="next-steps"></a>Próximas etapas

- [Criar e executar um notebook do Kusto](../notebooks/notebooks-kusto-kernel.md)
- [Notebook Kqlmagic no Azure Data Studio](../notebooks/notebooks-kqlmagic.md)
- [Roteiro do SQL para o Kusto](/azure/data-explorer/kusto/query/sqlcheatsheet)
- [O que é o Gerenciador de dados do Azure?](/azure/data-explorer/data-explorer-overview)
- [Como usar as visualizações do SandDance](https://sanddance.js.org/)
