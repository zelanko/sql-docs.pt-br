---
title: 'Lição 4 do tutorial de serviços de análise: criar relações | Microsoft Docs'
description: Descreve como criar relações no projeto do tutorial do Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 14bba10123ab1161b336934286e38a32fb351bf5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-relationships"></a>Criar relações

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você verificar as relações que foram criadas automaticamente quando você importou os dados e adicionar novas relações entre tabelas diferentes. Uma relação é uma conexão criada entre duas tabelas que estabelece como os dados dessas tabelas devem ser correlacionados. Por exemplo, a tabela DimProduct e a tabela DimProductSubcategory têm uma relação baseada no fato de que cada produto pertence a uma subcategoria. Para obter mais informações, consulte [relações](../tabular-models/relationships-ssas-tabular.md).
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 3: marcar como tabela de data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Revisar relações existentes e adicionar novas relações  

Quando você importar dados usando obter dados, você tem sete tabelas do banco de dados AdventureWorksDW. Em geral, quando você importa dados de uma fonte relacional, as relações existentes são importadas automaticamente junto com os dados. Para obter dados criar automaticamente relações no modelo de dados, deve haver relações entre tabelas na fonte de dados.

Antes de continuar a criar seu modelo, você deve verificar as relações entre tabelas foram criadas corretamente. Para este tutorial, você também adicionar três novas relações.  

  
#### <a name="to-review-existing-relationships"></a>Para revisar relações existentes  
  
1.  Clique o **modelo** menu > **exibição do modelo de** > **exibição de diagrama**.  

    O designer de modelo agora aparece na exibição de diagrama, um formato gráfico que exibe todas as tabelas que você importou com linhas entre elas. As linhas entre tabelas indicam as relações que foram criadas automaticamente quando você importar os dados.
    
    ![as-lesson4-diagram](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > Se você não vir as relações entre tabelas, provavelmente significa que não há nenhuma relação entre essas tabelas na fonte de dados.

    Inclua tantas tabelas quanto possível por meio de controles de minimapa no canto inferior direito do designer de modelo. Você também pode clicar e arrastar tabelas para locais diferentes, colocando-as mais próximas umas das outras ou colocando-as em uma ordem específica. Movendo tabelas não afeta as relações entre as tabelas. Para exibir todas as colunas em uma tabela específica, clique e arraste uma borda de tabela para expandir ou diminuí-lo.  
  
2.  Clique na linha sólida entre o **DimCustomer** tabela e o **DimGeography** tabela. A linha sólida entre essas duas tabelas mostra que essa relação está ativa, ou seja, que ele é usado por padrão quando o cálculo das fórmulas DAX.  
  
    Observe o **GeographyKey** coluna no **DimCustomer** tabela e o **GeographyKey** coluna o **DimGeography** agora aparecem cada dentro de uma caixa de tabela. Essas colunas são usadas na relação. Agora, as propriedades da relação também são exibidas na janela **Propriedades** .  
  
    > [!TIP]  
    > Você também pode usar a caixa de diálogo Gerenciar relações para mostrar as relações entre todas as tabelas em um formato de tabela. No Gerenciador de modelos de tabela, clique com botão direito **relações** > **gerenciar relações**.
  
3.  Verifique se as seguintes relações foram criadas quando cada uma das tabelas foi importada do banco de dados AdventureWorksDW:  
  
    |Ativa|Tabela|Tabela de Pesquisa Relacionada|  
    |----------|---------|------------------------|  
    |Sim|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sim|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sim|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sim|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sim|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se alguma das relações estiverem ausentes, verifique se o modelo inclui as seguintes tabelas: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se as tabelas da mesma conexão de fonte de dados são importadas em separado vezes, as relações entre essas tabelas não são criadas e devem ser criadas manualmente. Se nenhuma relação aparecer, isso significa que não há nenhuma relação na fonte de dados. Você pode criá-los manualmente no modelo de dados.

### <a name="take-a-closer-look"></a>Uma visão mais detalhada

Na exibição de diagrama, observe um número de linhas que mostram a relação entre tabelas, um asterisco e uma seta.

![as-lesson4-line](../tutorial-tabular-1400/media/as-lesson4-line.png)

A seta mostra a direção do filtro. O asterisco mostra esta tabela é a *muitos* lado da cardinalidade da relação e o mostra esta tabela é a *um* lado da relação. Se você precisar editar um relacionamento; Por exemplo, altere a direção da relação de filtro ou cardinalidade, clique duas vezes na linha da relação para abrir a caixa de diálogo Editar relação.

![as-lesson4-edit](../tutorial-tabular-1400/media/as-lesson4-edit.png)

Esses recursos destinam-se para modelagem de dados avançados e estão fora do escopo deste tutorial. Para obter mais informações, consulte [bidirecional entre os filtros para modelos de tabela no Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

Em alguns casos, talvez seja necessário criar relações adicionais entre tabelas no modelo para oferecer suporte a uma lógica corporativa específica. Para este tutorial, você precisa criar três relações adicionais entre as tabelas FactInternetSales e a tabela DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Para adicionar novas relações entre tabelas  
  
1.  No designer de modelo, no **FactInternetSales** de tabela, clique e mantenha o **OrderDate** coluna, em seguida, arraste o cursor para o **data** coluna o **DimDate** da tabela e, em seguida, solte.  

    Uma linha sólida aparece, indicando que você criou uma relação ativa entre o **OrderDate** coluna o **vendas pela Internet** tabela e o **data** coluna o **data** tabela. 
  
      ![as-lesson4-new](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > Ao criar relações, a direção de filtro e de cardinalidade entre a tabela primária e a tabela de pesquisa relacionada é selecionada automaticamente.  
  
2.  No **FactInternetSales** , clique e mantenha o **DueDate** coluna, em seguida, arraste o cursor para o **data** coluna no **DimDate** de tabela e, em seguida, solte.  
  
    Uma linha pontilhada aparece, indicando que você criou uma relação inativa entre a **DueDate** coluna o **FactInternetSales** tabela e o **data** coluna o **DimDate** tabela. Você pode ter várias relações entre tabelas, mas só uma relação pode estar ativa por vez. Relações inativas podem se tornar ativas para executar agregações especiais em expressões DAX personalizadas.  
  
3.  Finalmente, crie mais uma relação. No **FactInternetSales** , clique e mantenha o **ShipDate** coluna, em seguida, arraste o cursor para o **data** coluna no **DimDate** de tabela e, em seguida, solte.  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 5: Criar colunas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).
  
  
  
