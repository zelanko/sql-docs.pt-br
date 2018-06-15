---
title: 'Tutorial: Habilitar o tabela uso exemplo insight o widget espaço no Studio de operações do SQL (visualização) | Microsoft Docs'
description: Este tutorial demonstra como habilitar o tabela uso exemplo insight o widget espaço no painel de banco de dados do SQL Studio de operações (visualização).
ms.custom: tools|sos
ms.date: 03/19/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a09dd273bb005432eaf638bb88c55ff35a5bd90
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235256"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Tutorial: Habilitar a tabela espaço uso exemplo insight widget [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Este tutorial demonstra como habilitar um widget de informações no painel de banco de dados, fornecendo uma exibição de uma visão geral sobre o uso do espaço para todas as tabelas em um banco de dados. Durante este tutorial, você aprenderá como:

> [!div class="checklist"]
> * Ativar rapidamente um widget de informações usando um exemplo de widget de visão interna
> * Exibir os detalhes de uso de espaço de tabela
> * Filtrar dados e exibir os detalhes de rótulo em um gráfico de análise

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados do SQL Azure *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos tutoriais a seguir:

- [Conectar e consultar usando o SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Ativar um insight management no [!INCLUDE[name-sos](../includes/name-sos-short.md)]do painel de banco de dados
[!INCLUDE[name-sos](../includes/name-sos-short.md)] tem um widget de exemplo interno para monitorar o espaço usado por tabelas em um banco de dados.

1. Abra *as configurações do usuário* pressionando **Ctrl + Shift + P** para abrir o *comando paleta*.
2. Tipo *configurações* na caixa de pesquisa e selecione **preferências: Abrir configurações de usuário**.
2. Tipo *painel* na pesquisa de configurações de caixa de entrada e localize **dashboard.database.widgets**.

3. Para personalizar o **dashboard.database.widgets** configurações que você precisa editar o **dashboard.database.widgets** entrada no **as configurações do usuário** seção (a coluna o lado direito). Se não houver nenhum **dashboard.database.widgets** no **as configurações do usuário** seção, passe o mouse sobre o **dashboard.database.widgets** texto na coluna de configurações padrão e clique em o ícone de lápis que aparece à esquerda do texto e clique em **cópia configurações**. Se o pop-up informando **substituir nas configurações**, não clique nele! Vá para o **as configurações do usuário** coluna à direita e localize o **dashboard.database.widgets** seção e Avançar para a próxima etapa.

4. No **dashboard.database.widgets** seção, adicione o seguinte:

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```
O **dashboard.database.widgets** seção deve ser semelhante à seguinte imagem:

   ![Configurações de pesquisa](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. Pressione **Ctrl + S** para salvar as configurações.

6. Painel de banco de dados aberto clicando **TutorialDB** e clique em **gerenciar**.

7. Exibição de *espaço de tabela* widget insight conforme mostrado na imagem a seguir: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Trabalhando com o gráfico de análise

[!INCLUDE[name-sos](../includes/name-sos-short.md)]do gráfico insight fornece detalhes de filtragem e o foco de mouse. Tente as seguintes etapas:

1. Clique em e alternar o *row_count* legenda no gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] mostra e oculta a série de dados como uma legenda é ativar ou desativar.
    
2. Passe o ponteiro do mouse sobre o gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] mostra mais informações sobre o rótulo da série de dados e seu valor, conforme mostrado na seguinte captura de tela.

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