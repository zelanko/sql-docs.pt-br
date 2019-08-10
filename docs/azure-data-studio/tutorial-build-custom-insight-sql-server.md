---
title: 'Tutorial: Criar um widget de insight personalizado'
titleSuffix: Azure Data Studio
description: Este tutorial demonstra como criar widgets de insights personalizados e adicioná-los aos painéis de banco de dados e de servidor no Azure Data Studio.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 34ee9c23569897247f05d6b9b5f9f2610f5d68fc
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959095"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>Tutorial: Criar um widget de insight personalizado

Este tutorial demonstra como usar suas próprias consultas de insight para criar widgets de insight personalizados.

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Executar sua própria consulta e exibi-la em um gráfico
> * Criar um widget de insight personalizado usando o gráfico
> * Adicionar o gráfico a um painel de servidor ou de banco de dados
> * Adicionar detalhes ao widget de insight personalizado

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou o *TutorialDB* do Banco de Dados SQL do Azure. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

- [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar o Banco de Dados SQL do Azure usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>Executar sua própria consulta e exibir o resultado em um gráfico
Nesta etapa, execute um script SQL para consultar as sessões ativas atuais.

1. Para abrir um novo editor, pressione **Ctrl + N**. 

2. Altere o contexto de conexão para **TutorialDB**.

3. Cole a consulta a seguir no editor de consultas:

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. Salve a consulta no editor em um arquivo \*.sql. Para este tutorial, salve o script como *activeSession.sql*.

5. Para executar a consulta, pressione **F5**.

6. Depois que os resultados da consulta forem exibidos, clique em **Exibir como Gráfico** e, em seguida, clique na guia **Visualizador de Gráfico**.

7. Altere o **Tipo de Gráfico** para **contagem**. Essas configurações renderizam um gráfico de contagem.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>Adicione o insight personalizado ao painel do banco de dados

1. Para abrir a configuração do widget de insight, clique em **Criar Insight** no *Visualizador de Gráfico*:

   ![configuração](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. Copie a configuração do insight (os dados JSON). 

3. Pressione **Ctrl + vírgula** para abrir as *Configurações do Usuário*.

4. Digite *dashboard* nas *Configurações de Pesquisa*.

5. Clique em **Editar** para *dashboard.database.widgets*.

   ![configurações do painel](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. Cole do JSON de configuração do insight em *dashboard.database.widgets*. As configurações do painel do banco de dados são parecidas com as seguintes:

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

7. Salve o arquivo *Configurações do Usuário* e abra o painel do banco de dados *TutorialDB* para ver o widget de sessões ativas:

   ![insight de activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>Adicionar detalhes ao insight personalizado

1. Para abrir um novo editor, pressione **Ctrl + N**.

2. Altere o contexto de conexão para **TutorialDB**.

3. Cole a consulta a seguir no editor de consultas:

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. Salve a consulta no editor em um arquivo \*.sql. Para este tutorial, salve o script como *activeSessionDetail.sql*.

5. Pressione **Ctrl + vírgula** para abrir as *Configurações do Usuário*.

6. Edite o nó *dashboard.database.widgets* existente em seu arquivo de configurações:

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

7. Salve o arquivo *Configurações do Usuário* e abra o painel do banco de dados *TutorialDB*. Clique no botão de reticências (...) ao lado de *Meu Widget* para mostrar os detalhes:

    ![insight de activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Executar sua própria consulta e exibi-la em um gráfico
> * Criar um widget de insight personalizado usando o gráfico
> * Adicionar o gráfico a um painel de servidor ou de banco de dados
> * Adicionar detalhes ao widget de insight personalizado

Para saber como fazer backup e restaurar bancos de dados, conclua o próximo tutorial:

> [!div class="nextstepaction"]
> [Backup e restauração de bancos de dados](tutorial-backup-restore-sql-server.md).
