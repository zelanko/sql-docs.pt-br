---
title: 'Tutorial: Compilar um widget de visão personalizada no estúdio de dados do Azure | Microsoft Docs'
description: Este tutorial demonstra como compilar widgets de Insights personalizados e adicioná-los ao banco de dados e servidor painéis no estúdio de dados do Azure.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: caecf780f5c8cc656f6b0b2a95dd3d68c48355cb
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356337"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>Tutorial: Compilar um widget de visão personalizada

Este tutorial demonstra como usar suas próprias consultas de análise para compilar widgets insight personalizado.

Durante este tutorial, você aprenderá como:
> [!div class="checklist"]
> * Execute sua própria consulta e exibi-lo em um gráfico
> * Criar um widget de visão personalizada do gráfico
> * Adicione o gráfico a um painel de controle de servidor ou banco de dados
> * Adicionar detalhes ao seu widget insight personalizado

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados SQL *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos seguintes inícios rápidos:

- [Conectar e consultar usando SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>Execute sua própria consulta e exibir o resultado em uma exibição de gráfico
Nesta etapa, execute um script sql para consultar as sessões ativas atuais.

1. Para abrir um novo editor, pressione **Ctrl + N**. 

2. Alterar o contexto de conexão para **TutorialDB**.

3. Cole a seguinte consulta no editor de consultas:

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. Salve a consulta no editor para um \*arquivo. SQL. Para este tutorial, salve o script como *activeSession.sql*.

5. Para executar a consulta, pressione **F5**.

6. Depois que os resultados da consulta são exibidos, clique em **exibir como gráfico**, em seguida, clique no **Visualizador gráfico** guia.

7. Alteração **tipo de gráfico** à **contagem**. Essas configurações de renderizam um gráfico de contagem.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>Adicione o insight personalizado para o painel de banco de dados

1. Para abrir a configuração do widget de insight, clique em **criar Insight** nos *Visualizador gráfico*:

   ![configuração](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. Copie a configuração de informações (os dados JSON). 

3. Pressione **Ctrl + vírgula** para abrir *configurações do usuário*.

4. Tipo de *dashboard* na *as configurações de pesquisa*.

5. Clique em **edite** para *dashboard.database.widgets*.

   ![configurações do Dashboard](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. Cole a configuração de insight JSON em *dashboard.database.widgets*. Banco de dados o painel configurações é semelhante ao seguinte:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql"
                }
            }
        }
    ]
   ```

7. Salvar a *as configurações de usuário* e abra o *TutorialDB* painel de banco de dados para ver o widget de sessões ativas:

   ![activesession insight](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>Adicionar detalhes ao insight personalizado

1. Para abrir um novo editor, pressione **Ctrl + N**.

2. Alterar o contexto de conexão para **TutorialDB**.

3. Cole a seguinte consulta no editor de consultas:

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. Salve a consulta no editor para um \*arquivo. SQL. Para este tutorial, salve o script como *activeSessionDetail.sql*.

5. Pressione **Ctrl + vírgula** para abrir *configurações do usuário*.

6. Editar as existentes *dashboard.database.widgets* nó no arquivo de configurações:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. Salvar a *as configurações de usuário* e abra o *TutorialDB* painel de banco de dados. Clique no botão de reticências (...) ao lado *Meus Widget* para mostrar os detalhes:

    ![activesession insight](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Execute sua própria consulta e exibi-lo em um gráfico
> * Criar um widget de visão personalizada do gráfico
> * Adicione o gráfico a um painel de controle de servidor ou banco de dados
> * Adicionar detalhes ao seu widget insight personalizado

Para saber como fazer backup e restaurar bancos de dados, conclua o próximo tutorial:

> [!div class="nextstepaction"]
> [Fazer backup e restaurar bancos de dados](tutorial-backup-restore-sql-server.md).
