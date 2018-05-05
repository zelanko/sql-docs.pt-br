---
title: 'Tutorial: Exemplo de consultas mais lentas de habilitar os cinco widget - Studio de operações do SQL (visualização) | Microsoft Docs'
description: Este tutorial demonstra como habilitar o widget de exemplo de consultas mais lentos cinco no painel de banco de dados.
ms.custom: tools|sos
ms.date: 03/15/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.openlocfilehash: d06bd752b0cdd07d87d8e5816a74d6e2d43d31ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Adicionar o *cinco consultas mais lentas* widget de exemplo para o painel de banco de dados

Este tutorial demonstra o processo de adição de um dos [!INCLUDE[name-sos](../includes/name-sos-short.md)]do widgets internos de exemplo para o *painel de banco de dados* para exibir rapidamente as consultas mais lentas cinco de um banco de dados. Você também aprenderá como exibir os detalhes das consultas lentas e planos de consulta usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]de recursos. Durante este tutorial, você aprenderá como:

> [!div class="checklist"]
> * Habilitar o repositório de consultas em um banco de dados
> * Adicionar um widget insight pré-criado no painel de banco de dados
> * Exibir detalhes sobre as consultas mais lentas do banco de dados
> * Exibir planos de execução de consulta para as consultas lentas

[!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui várias insight widgets-de-prontos. Este tutorial mostra como adicionar o *consulta-data-armazenamento-db-insight* widget, mas as etapas são basicamente os mesmos para adicionar qualquer widget.

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados do SQL Azure *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos tutoriais a seguir:

- [Conectar e consultar usando o SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Ativar o repositório de consultas para seu banco de dados

O widget neste exemplo requer *repositório de consultas* para ser habilitado.

1. Clique com botão direito do **TutorialDB** banco de dados (no **servidores** barra lateral) e selecione **nova consulta**.
2. Cole a seguinte instrução Transact-SQL (T-SQL) no editor de consultas e, em seguida, clique em **executar**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Adicionar o widget de consultas lentas ao seu painel de banco de dados

Para adicionar o *lenta widget de consultas* para seu painel, edite o *dashboard.database.widgets* configuração seu *as configurações do usuário* arquivo.

1. Abra *as configurações do usuário* pressionando **Ctrl + Shift + P** para abrir o *comando paleta*.
2. Tipo *configurações* na caixa de pesquisa e selecione **preferências: Abrir configurações de usuário**.

   ![Comando de configurações de usuário abertas](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Tipo *painel* na pesquisa configurações caixa e localize **dashboard.database.widgets**.

   ![Configurações de pesquisa](./media/tutorial-qds-sql-server/search-settings.png)

3. Para personalizar o **dashboard.database.widgets** configurações que você precisa editar o **dashboard.database.widgets** entrada no **as configurações do usuário** seção (a coluna o lado direito). Se não houver nenhum **dashboard.database.widgets** no **as configurações do usuário** seção, passe o mouse sobre o **dashboard.database.widgets** texto na coluna de configurações padrão e clique em o ícone de lápis que aparece à esquerda do texto e clique em **cópia configurações**. Se o pop-up informando **substituir nas configurações**, não clique nele! Vá para o **as configurações do usuário** coluna à direita e localize o **dashboard.database.widgets** seção e Avançar para a próxima etapa.

4. No **dashboard.database.widgets** seção, adicione o seguinte:

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

1. Se esta for a primeira vez que adicionar um novo widget, o **dashboard.database.widgets** seção deve ser semelhante a este:

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

1. Pressione **Ctrl + S** para salvar o **as configurações de usuário**.

6. Abra o *painel de banco de dados* navegando até **TutorialDB** no **servidores** barra lateral, com o botão direito e selecione **gerenciar**.

   ![Abrir o painel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. O widget insight é exibido no painel: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Exibir detalhes de informações para obter mais informações

1. Para obter informações adicionais sobre um widget de análise, clique nas reticências (**...** ) no canto superior direito e selecione **Mostrar detalhes**.
2. Para mostrar mais detalhes sobre um item, selecione qualquer item na **dados do gráfico** lista.

   ![Caixa de diálogo de detalhe de informações](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Clique na célula à direita do **query_sql_txt** na **detalhes do Item** e clique em **Copiar célula**.

4. Fechar o **Insights** painel.

## <a name="view-the-query-plan"></a>Exibir o plano de consulta 

1. Abra um novo editor de consulta pressionando **Ctrl + N**.

2. Cole o texto da consulta nas etapas anteriores no editor.

3. Clique em **explicam**.

   ![Explique Insight QDS](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Exiba plano de execução da consulta:

   ![plano de execução](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Salvar e abrir um plano de consulta 

1. Abra a caixa de diálogo de detalhe de informações.
2. Selecione um dos itens de consulta.
2. Clique com botão direito **query_plan** valor e selecione **Copiar célula**

   ![Insights QDS plano](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Pressione **Ctrl + N** para abrir um novo editor.

4. Cole o plano copiado no editor.

5. Pressione **Ctrl + S** para salvar o arquivo e alterar a extensão de arquivo para *. sqlplan*. *sqlplan* não aparecer na lista suspensa de extensão de arquivo, portanto, basta digitá-la. Para este tutorial, nomeie o arquivo *slowquery.sqlplan*.

6. O plano de consulta é aberto no [!INCLUDE[name-sos](../includes/name-sos-short.md)]do Visualizador de plano de consulta:

   ![Insights QDS plano](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Habilitar o repositório de consultas em um banco de dados
> * Adicionar um widget de análise para o painel de banco de dados
> * Exibir detalhes sobre as consultas mais lentas do banco de dados
> * Exibir planos de execução de consulta para as consultas lentas


Para saber como habilitar o **uso do espaço de tabela** insight de exemplo, conclua o seguinte tutorial:

> [!div class="nextstepaction"]
> [Habilitar o widget de insight de exemplo de espaço de tabela](tutorial-table-space-sql-server.md)