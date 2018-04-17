---
title: 'Tutorial: Criar um widget de informações personalizadas no SQL Operations Studio (preview) | Microsoft Docs'
description: Este tutorial demonstra como compilar widgets insight personalizados e adicioná-los ao banco de dados e servidor painéis no SQL Operations Studio (preview).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 344cf021a4a0abc13fc8c531875c604095c8c0d1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-build-a-custom-insight-widget"></a>Tutorial: Criar um widget de informações personalizadas

Este tutorial demonstra como usar suas próprias consultas de análise para compilar widgets de informações personalizadas.

Durante este tutorial, você aprenderá como:
> [!div class="checklist"]
> * Executar sua consulta e exibi-lo em um gráfico
> * Criar um widget insight personalizado do gráfico
> * Adicione o gráfico a um painel do servidor ou banco de dados
> * Adicionar detalhes para o widget insight personalizado

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados do SQL Azure *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos tutoriais a seguir:

- [Conectar e consultar usando o SQL Server[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>Executar sua consulta e exibir o resultado em uma exibição de gráfico
Nesta etapa, execute um script sql para consultar as sessões ativas atuais.

1. Para abrir um novo editor, pressione **Ctrl + N**. 

2. Alterar o contexto de conexão para **TutorialDB**.

3. Cole a seguinte consulta no editor de consultas:

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. Salvar a consulta no editor para um \*arquivo. SQL. Para este tutorial, salve o script como *activeSession.sql*.

5. Para executar a consulta, pressione **F5**.

6. Depois que os resultados da consulta são exibidos, clique em **exibição como gráfico**, em seguida, clique no **Visualizador gráfico** guia.

7. Alterar **tipo de gráfico** para **contagem**. Essas configurações renderizam um gráfico de contagem.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>Adicione o insight personalizado para o painel de banco de dados

1. Para abrir a configuração do widget insight, clique em **criar Insight** na *Visualizador gráfico*:

   ![configuração](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. Copie a configuração de informações (os dados JSON). 

3. Pressione **Ctrl + vírgula** abrir *as configurações de usuário*.

4. Tipo *painel* na *as configurações de pesquisa*.

5. Clique em **editar** para *dashboard.database.widgets*.

   ![Configurações do Dashboard](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. Cole a informações de configuração JSON em *dashboard.database.widgets*. Banco de dados painel configurações é semelhante ao seguinte:

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

7. Salve o *as configurações do usuário* de arquivo e abra o *TutorialDB* painel para ver o widget de sessões ativas do banco de dados:

   ![análise de activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>Adicionar detalhes ao insight personalizado

1. Para abrir um novo editor, pressione **Ctrl + N**.

2. Alterar o contexto de conexão para **TutorialDB**.

3. Cole a seguinte consulta no editor de consultas:

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. Salvar a consulta no editor para um \*arquivo. SQL. Para este tutorial, salve o script como *activeSessionDetail.sql*.

5. Pressione **Ctrl + vírgula** abrir *as configurações de usuário*.

6. Editar existente *dashboard.database.widgets* nó no seu arquivo de configurações:

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

7. Salve o *as configurações do usuário* de arquivo e abra o *TutorialDB* painel de banco de dados. Clique no botão de reticências (...) ao lado de *Meus Widget* para mostrar os detalhes:

    ![análise de activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Executar sua consulta e exibi-lo em um gráfico
> * Criar um widget insight personalizado do gráfico
> * Adicione o gráfico a um painel do servidor ou banco de dados
> * Adicionar detalhes para o widget insight personalizado

Para saber como fazer backup e restaurar bancos de dados, conclua o seguinte tutorial:

> [!div class="nextstepaction"]
> [Fazer backup e restaurar bancos de dados](tutorial-backup-restore-sql-server.md).