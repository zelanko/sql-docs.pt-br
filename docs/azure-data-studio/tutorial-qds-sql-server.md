---
title: 'Tutorial: Habilitar o widget de exemplo de consultas mais lentas cinco'
titleSuffix: Azure Data Studio
description: Este tutorial demonstra como habilitar o widget de exemplo de consultas mais lentas cinco no painel de banco de dados.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 5c94d2cf8b80ad7724cc1f710dc67d3f4a13c59e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959061"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Adicione a *cinco consultas mais lentas* widget de exemplo para o painel de banco de dados

Este tutorial demonstra o processo de adição de uma [!INCLUDE[name-sos](../includes/name-sos-short.md)]do widgets internos de exemplo para o *painel de banco de dados* para exibir rapidamente os cinco consultas mais lentas de um banco de dados. Você também aprenderá a exibir os detalhes das consultas lentas e planos de consulta usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]de recursos. Durante este tutorial, você aprenderá como:

> [!div class="checklist"]
> * Habilitar a consulta Store em um banco de dados
> * Adicionar um widget de insight pré-criados para o painel de banco de dados
> * Exibir detalhes sobre as consultas mais lentas do banco de dados
> * Exibir planos de execução de consulta para as consultas lentas

[!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui vários insight widgets out-of-the-box. Este tutorial mostra como adicionar o *-dados-store-db-análise de consultas* widget, mas as etapas são basicamente as mesmas para adicionar qualquer widget.

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados SQL *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos seguintes inícios rápidos:

- [Conectar e consultar usando SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Ativar Store de consulta do banco de dados

O widget neste exemplo exige *Store consulta* esteja habilitado.

1. Clique com botão direito do **TutorialDB** banco de dados (na **servidores** barra lateral) e selecione **nova consulta**.
2. Cole a seguinte instrução Transact-SQL (T-SQL) no editor de consultas e, em seguida, clique em **executar**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Adicionar o widget de consultas lentas ao seu painel de banco de dados

Para adicionar o *lento o widget de consultas* ao seu painel, edite o *dashboard.database.widgets* definindo no seu *configurações de usuário* arquivo.

1. Abra *as configurações de usuário* pressionando **Ctrl + Shift + P** para abrir o *paleta de comandos*.
2. Tipo de *as configurações* na caixa de pesquisa e selecione **preferências: Abrir configurações de usuário**.

   ![Comando de configurações do usuário abertas](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Tipo de *dashboard* na pesquisa configurações caixa e localize **dashboard.database.widgets**.

   ![Configurações de pesquisa](./media/tutorial-qds-sql-server/search-settings.png)

3. Para personalizar o **dashboard.database.widgets** as configurações que você precisa editar o **dashboard.database.widgets** entrada no **configurações de usuário** seção (a coluna no lado direito). Se não houver nenhuma **dashboard.database.widgets** na **configurações do usuário** seção, passe o mouse sobre o **dashboard.database.widgets** texto na coluna de configurações padrão e clique em o ícone de lápis que aparece à esquerda do texto e clique em **cópia configurações**. Se o pop-up diz **substituir nas configurações**, não clique nele! Vá para o **as configurações de usuário** coluna à direita e localize o **dashboard.database.widgets** seção e vá para a próxima etapa.

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

1. Se esta for a primeira vez adicionando um novo widget, o **dashboard.database.widgets** seção deve ser semelhante a esta:

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

1. Pressione **Ctrl + S** para salvar o modificado **configurações do usuário**.

6. Abra o *painel de banco de dados* navegando até **TutorialDB** no **servidores** barra lateral, o botão direito do mouse e selecione **gerenciar**.

   ![Abrir o painel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. O widget de insight é exibido no painel: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Exibir detalhes de informações para obter mais informações

1. Para exibir informações adicionais sobre um widget de insight, clique nas reticências ( **...** ) no canto superior direito e selecione **Mostrar detalhes**.
2. Para mostrar mais detalhes para um item, selecione qualquer item na **dados do gráfico** lista.

   ![Caixa de diálogo de detalhe de Insight](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. A célula à direita do botão direito do mouse **query_sql_txt** na **detalhes do Item** e clique em **Copiar célula**.

4. Fechar o **Insights** painel.

## <a name="view-the-query-plan"></a>Exibir o plano de consulta 

1. Abra um novo editor de consulta pressionando **Ctrl + N**.

2. Cole o texto da consulta das etapas anteriores no editor.

3. Clique em **Explique**.

   ![Explique Insight QDS](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Exiba plano de execução da consulta:

   ![plano de execução](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Salvar e abrir um plano de consulta 

1. Abra a caixa de diálogo de detalhe de informações.
2. Selecione um dos itens de consulta.
2. Clique com botão direito **query_plan** de valor e selecione **Copiar célula**

   ![Plano do Insights QDS](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Pressione **Ctrl + N** para abrir um novo editor.

4. Cole o plano copiado no editor.

5. Pressione **Ctrl + S** para salvar o arquivo e altere a extensão de arquivo para *. sqlplan*. *. sqlplan* não aparecer na lista suspensa de extensão de arquivo, então, basta digitá-lo no. Para este tutorial, nomeie o arquivo *slowquery.sqlplan*.

6. O plano de consulta é aberto no [!INCLUDE[name-sos](../includes/name-sos-short.md)]do Visualizador de plano de consulta:

   ![Plano do Insights QDS](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Habilitar a consulta Store em um banco de dados
> * Adicionar um widget de visão para o painel de banco de dados
> * Exibir detalhes sobre as consultas mais lentas do banco de dados
> * Exibir planos de execução de consulta para as consultas lentas


Para saber como habilitar a **uso do espaço de tabela** amostra de insight, conclua o próximo tutorial:

> [!div class="nextstepaction"]
> [Habilitar o widget de insight de exemplo de espaço de tabela](tutorial-table-space-sql-server.md)
