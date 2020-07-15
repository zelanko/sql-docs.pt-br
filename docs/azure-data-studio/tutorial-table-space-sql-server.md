---
title: Habilitar o widget de insight de exemplo de uso do espaço de tabela
description: Este tutorial demonstra como habilitar o widget de insight de exemplo de uso do espaço de tabela no painel de banco de dados do Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/10/2019
ms.openlocfilehash: 8d2be24a72c098c5a6a0b5e3ecefbde9bbe39cd5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726699"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-azure-data-studio"></a>Tutorial: Habilitar o widget de insight de exemplo de uso do espaço de tabela usando Azure Data Studio

Este tutorial demonstra como habilitar um widget de insight no painel de banco de dados, fornecendo uma visão geral do uso do espaço para todas as tabelas de um banco de dados. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Ativar rapidamente um widget de insight usando um exemplo de widget de insight interno
> * Exibir os detalhes do uso do espaço de tabela
> * Filtrar dados e exibir detalhes do rótulo em um gráfico de insight

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer o SQL Server ou o *TutorialDB* do Banco de Dados SQL do Azure. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

* [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
* [Conectar e consultar o Banco de Dados SQL do Azure usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)

## <a name="turn-on-a-management-insight-on-azure-data-studios-database-dashboard"></a>Ativar um insight de gerenciamento no painel de banco de dados do Azure Data Studio

O Azure Data Studio tem um widget de exemplo interno para monitorar o espaço usado pelas tabelas em um banco de dados.

1. Abra as *Configurações do Usuário* pressionando **Ctrl+Shift+P** para abrir a *Paleta de Comandos*.

2. Digite *configurações* na caixa de pesquisa e selecione **Preferências: Abrir Configurações do Usuário**.

3. Digite *dashboard* na caixa de Pesquisa de Configurações e localize **dashboard.database.widgets**.

4. Para personalizar as configurações de **dashboard.database.widgets**, é necessário editar a entrada **dashboard.database.widgets** na seção **CONFIGURAÇÕES DO USUÁRIO**.

   ![Pesquisar configurações](media/tutorial-table-space-sql-server/search-settings.png)

   Se não houver um **dashboard.database.widgets** na seção **CONFIGURAÇÕES DO USUÁRIO**, passe o mouse sobre o texto **dashboard.database.widgets** na coluna CONFIGURAÇÕES PADRÃO, clique no ícone de *engrenagem* que aparece à esquerda do texto e clique em **Copiar como JSON de Configuração**. Se o pop-up disser **Substituir nas Configurações**, não clique! Vá para a coluna **CONFIGURAÇÕES DO USUÁRIO** à direita e localize a seção **dashboard.database.widgets** e avance para a próxima etapa.

5. Na seção **dashboard.database.widgets**, adicione as seguintes linhas:

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

   A seção **dashboard.database.widgets** deve ser semelhante à seguinte imagem:

    ![Pesquisar configurações](./media/tutorial-table-space-sql-server/insight-table-space.png)

6. Pressione **Ctrl + S** para salvar as configurações.

7. Abra o painel do banco de dados clicando com o botão direito do mouse em **TutorialDB** e clique em **Gerenciar**.

8. Exiba o widget de insight de *espaço de tabela*, conforme mostrado na imagem a seguir:

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)

## <a name="working-with-the-insight-chart"></a>Trabalhando com o gráfico de insight

O gráfico de insights do Azure Data Studio fornece filtragem e detalhes da focalização do mouse. Para testar, siga estas etapas:

1. Clique e alterne a legenda *row_count* no gráfico. O Azure Data Studio mostra e oculta a série de dados à medida que você alterna ou desativa uma legenda.

2. Passe o ponteiro do mouse sobre o gráfico. O Azure Data Studio mostra mais informações sobre o rótulo da série de dados e o valor dele, conforme mostrado na captura de tela a seguir.

   ![alternância de gráfico e legenda](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Ativar rapidamente um widget de insight usando um exemplo de widget de insight interno.
> * Exibir os detalhes do uso do espaço de tabela.
> * Filtrar dados e exibir detalhes do rótulo em um gráfico de insight

Para saber como criar um widget de insight personalizado, conclua o próximo tutorial:

> [!div class="nextstepaction"]
> [Criar um widget de insight personalizado](tutorial-build-custom-insight-sql-server.md)
