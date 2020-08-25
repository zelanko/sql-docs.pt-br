---
title: Habilitar o widget de exemplo das cinco consultas mais lentas
description: Este tutorial demonstra como habilitar o widget de exemplo das cinco consultas mais lentas no painel do banco de dados.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 06/01/2020
ms.openlocfilehash: 678d985daf2ca3130fbf7eb3b052718c3cc898ab
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746186"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Adicionar o widget de exemplo das *cinco consultas mais lentas* ao painel do banco de dados

Este tutorial demonstra o processo de adicionar um dos widgets de exemplo internos do Azure Data Studio ao *painel do banco de dados* para exibir rapidamente as cinco consultas mais lentas de um banco de dados. Você também aprenderá a ver os detalhes das consultas lentas e os planos de consulta usando os recursos do Azure Data Studio. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Habilitar Repositório de Consultas em um banco de dados
> * Adicionar um widget de insight predefinido ao painel do banco de dados
> * Exibir detalhes sobre as consultas mais lentas do banco de dados
> * Exibir os planos de execução de consulta para as consultas lentas

O Azure Data Studio inclui vários widgets de insights prontos para uso. Este tutorial mostra como adicionar o widget *query-data-store-db-insight*, mas as etapas são basicamente as mesmas para adicionar qualquer widget.

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer o SQL Server ou o *TutorialDB* do Banco de Dados SQL do Azure. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

* [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

* [Conectar e consultar o Banco de Dados SQL do Azure usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)

## <a name="turn-on-query-store-for-your-database"></a>Ativar o Repositório de Consultas para seu banco de dados

O widget neste exemplo requer que o *Repositório de Consultas* esteja habilitado.

1. Clique com o botão direito do mouse no banco de dados **TutorialDB** (na barra lateral **SERVIDORES**) e selecione **Nova Consulta**.

2. Cole a seguinte instrução T-SQL (Transact-SQL) no editor de consultas e clique em **Executar**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Adicionar o widget de consultas lentas ao painel do banco de dados

Para adicionar o *widget de consultas lentas* ao seu painel, edite a configuração *dashboard.database.widgets* em seu arquivo de *Configurações do Usuário*.

1. Abra as *Configurações do Usuário* pressionando **Ctrl+Shift+P** para abrir a *Paleta de Comandos*.

2. Digite *configurações* na caixa de pesquisa e selecione **Preferências: Abrir Configurações do Usuário**.

   ![Comando Abrir configurações do usuário](./media/tutorial-qds-sql-server/open-user-settings.png)

3. Digite *painel* na caixa de pesquisa de configurações e localize **dashboard.database.widgets**; em seguida, clique em *editar em settings.json*.

   ![Pesquisar configurações](./media/tutorial-qds-sql-server/search-settings.png)

4. Em settings.json, adicione o código abaixo a seguir:

   ```json
   "dashboard.database.widgets": [
       {
           "name": "slow queries widget",
           "gridItemConfig": {
               "sizex": 2,
               "sizey": 1
           },
           "widget": {
               "query-data-store-db-insight": null
           }
       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }
       }
   ]
   ```

5. Pressione **Ctrl + S** para salvar as **Configurações do Usuário** modificadas.

6. Abra o *Painel do banco de dados* navegando até **TutorialDB** na barra lateral **SERVIDORES**, clique com o botão direito do mouse e selecione **Gerenciar**.

   ![Abrir painel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. O widget de insight aparece no painel:

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)

## <a name="view-insight-details-for-more-information"></a>Exibir detalhes do insight para obter mais informações

1. Para exibir informações adicionais para um widget de insight, clique nas reticências ( **...** ) no canto superior direito e selecione **Exibir Detalhes**.

2. Para mostrar mais detalhes de um item, selecione qualquer item na lista **Dados do Gráfico**.

   ![Caixa de diálogo de detalhes do insight](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Feche o painel **Insights**.

## <a name="view-the-query-plan"></a>Exibir o plano de consulta

1. Clique com o botão direito do mouse no banco de dados **TutorialDB** e selecione *Gerenciar*

2. No *widget de consulta lenta* Para exibir mais informações para um widget de insight, clique nas reticências ( **...** ) no canto superior direito e selecione **Executar Consulta**.

    ![Executar Consulta](media/tutorial-qds-sql-server/run-query.png)

3. Agora você deve ver uma nova janela de consulta com os resultados.

    ![Resultados de Executar Consulta](media/tutorial-qds-sql-server/run-query-results.png)

4. Clique em **Explicar**.

   ![Explicação do QDS de insight](./media/tutorial-qds-sql-server/insight-qds-explain.png)

5. Exibir o plano de execução da consulta:

   ![plano de execução](./media/tutorial-qds-sql-server/showplan.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Habilitar Repositório de Consultas em um banco de dados
> * Adicionar um widget de insight ao painel do banco de dados
> * Exibir detalhes sobre as consultas mais lentas do banco de dados
> * Exibir os planos de execução de consulta para as consultas lentas

Para saber como habilitar o insight de exemplo de **uso do espaço de tabela**, siga o próximo tutorial:

> [!div class="nextstepaction"]
> [Habilitar o widget insight de exemplo de espaço de tabela](tutorial-table-space-sql-server.md)