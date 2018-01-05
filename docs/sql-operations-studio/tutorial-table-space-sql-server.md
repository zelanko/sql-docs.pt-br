---
title: "Tutorial: Habilitar o tabela uso exemplo insight o widget espaço no Studio de operações do SQL (visualização) | Microsoft Docs"
description: "Este tutorial demonstra como habilitar o tabela uso exemplo insight o widget espaço no painel de banco de dados do SQL Studio de operações (visualização)."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c51c7d1804baa490e665d316a08d911038c9f11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Tutorial: Habilitar a tabela espaço uso exemplo insight widget[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Este tutorial demonstra como habilitar um widget de informações no painel de banco de dados, fornecendo uma exibição de uma visão geral sobre o uso do espaço para todas as tabelas em um banco de dados. Durante este tutorial, você aprenderá como:

> [!div class="checklist"]
> * Ativar rapidamente um widget de informações usando um exemplo de widget de visão interna
> * Exibir os detalhes de uso de espaço de tabela
> * Filtrar dados e exibir os detalhes de rótulo em um gráfico de análise

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados do SQL Azure *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos tutoriais a seguir:

- [Conectar e consultar usando o SQL Server[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Ativar um insight management no [!INCLUDE[name-sos](../includes/name-sos-short.md)]do painel de banco de dados
[!INCLUDE[name-sos](../includes/name-sos-short.md)]tem um widget de exemplo interno para monitorar o espaço usado por tabelas em um banco de dados.

1. Abra **as configurações do usuário** pressionando **Ctrl + Shift + P** abrir *comando paleta*, tipo *configurações* na caixa de pesquisa e selecione  **Preferências: Abra as configurações do usuário**.

   ![Comando de configurações de usuário abertas](./media/tutorial-table-space-sql-server/open-user-settings.png)

2. Tipo *painel* na pesquisa de configurações de caixa de entrada e localize **dashboard.database.widgets**.

   ![Configurações de pesquisa](./media/tutorial-table-space-sql-server/search-settings.png)

3. Para personalizar o **dashboard.database.widgets** definir, passe o mouse sobre o ícone de lápis à esquerda do **dashboard.database.widgets** texto, clique em **editar**  >  **Cópia configurações**.

4. Usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]do IntelliSense, as configurações de informações configurar *nome* para o título do widget, *gridItemConfig* para o tamanho do widget, e *widget* selecionando **tabela espaço-db insight** da lista suspensa, conforme mostrado na seguinte captura de tela:

   ![Configurações de informações](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. Pressione **Ctrl + S** para salvar as configurações.

6. Painel de banco de dados aberto clicando **TutorialDB** e clique em **gerenciar**.

   ![Abrir o painel](./media/tutorial-table-space-sql-server/insight-open-dashboard.png)

7. Exibição *espaço usado por tabelas* conforme mostrado na seguinte captura de tela: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Trabalhando com o gráfico de análise

[!INCLUDE[name-sos](../includes/name-sos-short.md)]do gráfico insight fornece detalhes de filtragem e o foco de mouse. Tente as seguintes etapas:

1. Clique em e alternar o *row_count* legenda no gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)]mostra e oculta a série de dados como uma legenda é ativar ou desativar.
    
2. Passe o ponteiro do mouse sobre o gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)]mostra mais informações sobre o rótulo da série de dados e seu valor, conforme mostrado na seguinte captura de tela.

   ![alternância de gráfico e legenda](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Ative rapidamente um widget de informações usando uma amostra de widget de informações internas.
> * Exiba os detalhes de uso de espaço de tabela.
> * Filtrar dados e exibir os detalhes de rótulo em um gráfico de análise

Para saber como criar um widget de informações personalizadas, concluir o seguinte tutorial:

> [!div class="nextstepaction"]
> [Criar um widget insight personalizado](tutorial-build-custom-insight-sql-server.md).