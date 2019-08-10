---
title: 'Tutorial: Habilitar o widget de exemplo das cinco consultas mais lentas'
titleSuffix: Azure Data Studio
description: Este tutorial demonstra como habilitar o widget de exemplo das cinco consultas mais lentas no painel do banco de dados.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 5c94d2cf8b80ad7724cc1f710dc67d3f4a13c59e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959061"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Adicionar o widget de exemplo das *cinco consultas mais lentas* ao painel do banco de dados

Este tutorial demonstra o processo de adicionar um dos widgets de exemplo internos do [!INCLUDE[name-sos](../includes/name-sos-short.md)] ao *painel do banco de dados* para exibir rapidamente as cinco consultas mais lentas de um banco de dados. Você também aprenderá a exibir os detalhes das consultas lentas e os planos de consulta usando os recursos de [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Habilitar Repositório de Consultas em um banco de dados
> * Adicionar um widget de insight predefinido ao painel do banco de dados
> * Exibir detalhes sobre as consultas mais lentas do banco de dados
> * Exibir os planos de execução de consulta para as consultas lentas

[!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui vários widgets de insights prontos para uso. Este tutorial mostra como adicionar o widget *query-data-store-db-insight*, mas as etapas são basicamente as mesmas para adicionar qualquer widget.

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou o *TutorialDB* do Banco de Dados SQL do Azure. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

- [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar o Banco de Dados SQL do Azure usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



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

2. Digite *dashboard* na caixa de pesquisa de configurações e localize **dashboard.database.widgets**.

   ![Pesquisar configurações](./media/tutorial-qds-sql-server/search-settings.png)

3. Para personalizar as configurações de **dashboard.database.widgets**, você precisa editar a entrada **dashboard.database.widgets** na seção **CONFIGURAÇÕES DO USUÁRIO** (a coluna no lado direito). Se não houver um **dashboard.database.widgets** na seção **CONFIGURAÇÕES DO USUÁRIO**, passe o mouse sobre o texto **dashboard.database.widgets** na coluna CONFIGURAÇÕES PADRÃO, clique no ícone de lápis que aparece à esquerda do texto e clique em **Copiar para Configurações**. Se o pop-up disser **Substituir nas Configurações**, não clique! Vá para a coluna **CONFIGURAÇÕES DO USUÁRIO** à direita e localize a seção **dashboard.database.widgets** e avance para a próxima etapa.

4. Na seção **dashboard.database.widgets**, adicione o seguinte:

   ```json
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
    ```

1. Se esta for a primeira vez que você adiciona um novo widget, a seção **dashboard.database.widgets** deverá ser semelhante a esta:

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

1. Pressione **Ctrl + S** para salvar as **Configurações do Usuário** modificadas.

6. Abra o *Painel do banco de dados* navegando até **TutorialDB** na barra lateral **SERVIDORES**, clique com o botão direito do mouse e selecione **Gerenciar**.

   ![Abrir painel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. O widget de insight aparece no painel: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Exibir detalhes do insight para obter mais informações

1. Para exibir informações adicionais para um widget de insight, clique nas reticências ( **...** ) no canto superior direito e selecione **Exibir Detalhes**.
2. Para mostrar mais detalhes de um item, selecione qualquer item na lista **Dados do Gráfico**.

   ![Caixa de diálogo de detalhes do insight](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Clique com o botão direito do mouse na célula à direita de **query_sql_txt** em **Detalhes do Item** e clique em **Copiar Célula**.

4. Feche o painel **Insights**.

## <a name="view-the-query-plan"></a>Exibir o plano de consulta 

1. Abra um novo editor de consultas pressionando **Ctrl + N**.

2. Cole o texto da consulta das etapas anteriores no editor.

3. Clique em **Explicar**.

   ![Explicação do QDS de insight](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Exibir o plano de execução da consulta:

   ![plano de execução](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Salvar e abrir um plano de consulta 

1. Abra a caixa de diálogo de detalhes do insight.
2. Selecione um dos itens de consulta.
2. Clique com o botão direito do mouse no valor **query_plan** e selecione **Copiar Célula**

   ![Plano do QDS de insight](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Pressione **Ctrl + N** para abrir um novo editor.

4. Cole o plano copiado no editor.

5. Pressione **Ctrl + S** para salvar o arquivo e altere a extensão do arquivo para *.sqlplan*. *.sqlplan* não aparece na lista suspensa de extensões de arquivo, portanto, basta digitá-lo. Para este tutorial, dê ao arquivo o nome *slowquery.sqlplan*.

6. O plano de consulta é aberto no visualizador de plano de consulta de [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

   ![Plano do QDS de insight](./media/tutorial-qds-sql-server/sqlplan.png)


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
