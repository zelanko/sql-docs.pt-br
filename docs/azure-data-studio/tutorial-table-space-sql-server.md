---
title: 'Tutorial: Habilitar o tabela uso exemplo insight o widget espaço no estúdio de dados do Azure | Microsoft Docs'
description: Este tutorial demonstra como habilitar o tabela uso exemplo insight o widget espaço no painel de banco de dados do estúdio de dados do Azure.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 55d6c96cc328f21d1b51ce7186c8396ab278ee6f
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49355987"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Tutorial: Habilitar a tabela espaço uso exemplo insight widget [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Este tutorial demonstra como habilitar um widget de insight no painel do banco de dados, fornecendo uma exibição de uma visão geral sobre o uso do espaço para todas as tabelas em um banco de dados. Durante este tutorial, você aprenderá como:

> [!div class="checklist"]
> * Ativar rapidamente um widget de insight usando um exemplo de widget de visão interna
> * Exibir os detalhes de uso do espaço de tabela
> * Filtrar dados e exibir os detalhes de rótulo em um gráfico de insight

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados SQL *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos seguintes inícios rápidos:

- [Conectar e consultar usando SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Ativar-em um insight de gerenciamento [!INCLUDE[name-sos](../includes/name-sos-short.md)]do painel de banco de dados
[!INCLUDE[name-sos](../includes/name-sos-short.md)] traz um widget de exemplo internos para monitorar o espaço usado por tabelas em um banco de dados.

1. Abra *as configurações de usuário* pressionando **Ctrl + Shift + P** para abrir o *paleta de comandos*.
2. Tipo de *as configurações* na caixa de pesquisa e selecione **preferências: Abrir configurações de usuário**.
2. Tipo de *dashboard* na pesquisa de configurações de caixa de entrada e localize **dashboard.database.widgets**.

3. Para personalizar o **dashboard.database.widgets** as configurações que você precisa editar o **dashboard.database.widgets** entrada no **configurações de usuário** seção (a coluna no lado direito). Se não houver nenhuma **dashboard.database.widgets** na **configurações do usuário** seção, passe o mouse sobre o **dashboard.database.widgets** texto na coluna de configurações padrão e clique em o ícone de lápis que aparece à esquerda do texto e clique em **cópia configurações**. Se o pop-up diz **substituir nas configurações**, não clique nele! Vá para o **as configurações de usuário** coluna à direita e localize o **dashboard.database.widgets** seção e vá para a próxima etapa.

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

7. Modo de exibição de *espaço de tabela* widget de insight, conforme mostrado na imagem a seguir: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Trabalhando com o gráfico de insight

[!INCLUDE[name-sos](../includes/name-sos-short.md)]do gráfico de insight fornece detalhes de filtragem e ao passar o mouse. Para experimentar as etapas a seguir:

1. Clique em e ative/desative o *row_count* legenda no gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] mostra e oculta a série de dados como uma legenda é ligar ou desligar.
    
2. Passe o ponteiro do mouse sobre o gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] mostra mais informações sobre o rótulo de série de dados e seu valor, conforme mostrado na seguinte captura de tela.

   ![Ativar/desativar o gráfico e legenda](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Ative rapidamente um widget de insight usando uma amostra de widget de visão interna.
> * Exiba os detalhes de uso do espaço de tabela.
> * Filtrar dados e exibir os detalhes de rótulo em um gráfico de insight

Para saber como criar um widget de visão personalizada, conclua o próximo tutorial:

> [!div class="nextstepaction"]
> [Criar um widget personalizado insight](tutorial-build-custom-insight-sql-server.md).
