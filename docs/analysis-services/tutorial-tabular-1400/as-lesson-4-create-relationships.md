---
title: 'Analysis Services lição 4 do tutorial: Criar relações | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 16fcf8e5f85464dbba7666f0f4ebebba829405af
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685593"
---
# <a name="create-relationships"></a>Criar relações

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você verifica as relações que foram criadas automaticamente quando você importou dados e adicionar novas relações entre tabelas diferentes. Uma relação é uma conexão criada entre duas tabelas que estabelece como os dados dessas tabelas devem ser correlacionados. Por exemplo, a tabela DimProduct e a tabela DimProductSubcategory têm uma relação baseada no fato de que cada produto pertence a uma subcategoria. Para obter mais informações, consulte [relações](../tabular-models/relationships-ssas-tabular.md).
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 3: Marcar como tabela de data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Revisar relações existentes e adicionar novas relações  

Quando você importou dados por meio de obter dados, você obteve sete tabelas do banco de dados AdventureWorksDW. Em geral, quando você importa dados de uma fonte de dados relacional, as relações existentes são importadas automaticamente junto com os dados. Para obter dados criar automaticamente relações no modelo de dados que, deve haver relações entre tabelas na fonte de dados.

Antes de prosseguir com a criação de seu modelo, você deve verificar essas relações entre tabelas foram criadas corretamente. Para este tutorial, você também adicionará três novas relações.  

  
#### <a name="to-review-existing-relationships"></a>Para revisar relações existentes  
  
1.  Clique o **modelo** menu > **exibição de modelo** > **exibição de diagrama**.  

    O designer de modelo agora aparece na exibição de diagrama, um formato gráfico que exibe todas as tabelas você importou com linhas entre elas. As linhas entre tabelas indicam as relações que foram criadas automaticamente quando você importar os dados.
    
    ![as-lesson4-diagram](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > Se você não vir todas as relações entre tabelas, provavelmente significa que não há nenhuma relação entre essas tabelas na fonte de dados.

    Inclua o máximo de tabelas possível por meio de controles de minimapa no canto inferior direito do designer de modelo. Você também pode clicar e arrastar tabelas para locais diferentes, colocando-as mais próximas umas das outras ou colocando-as em uma ordem específica. A movimentação de tabelas não afeta as relações entre as tabelas. Para exibir todas as colunas em uma tabela específica, clique e arraste em uma borda de tabela para expandir ou diminuí-lo.  
  
2.  Clique na linha sólida entre a **DimCustomer** tabela e o **DimGeography** tabela. A linha sólida entre essas duas tabelas mostra que essa relação está ativa, ou seja, que ele é usado por padrão ao calcular fórmulas DAX.  
  
    Observe a **GeographyKey** coluna na **DimCustomer** tabela e o **GeographyKey** coluna no **DimGeography** tabela agora ambos cada um aparecem dentro de uma caixa. Essas colunas são usadas na relação. As propriedades da relação agora também aparecem na **propriedades** janela.  
  
    > [!TIP]  
    > Você também pode usar a caixa de diálogo Gerenciar relações para mostrar as relações entre todas as tabelas em um formato de tabela. No Gerenciador de modelos tabulares, clique com botão direito **relacionamentos** > **gerenciar relações**.
  
3.  Verifique se as seguintes relações foram criadas quando cada uma das tabelas foi importada do banco de dados AdventureWorksDW:  
  
    |Ativa|Table|Tabela de Pesquisa Relacionada|  
    |----------|---------|------------------------|  
    |Sim|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sim|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sim|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sim|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sim|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se qualquer uma das relações estiver ausente, verifique se que o modelo inclui as tabelas a seguir: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se as tabelas da mesma conexão de fonte de dados forem importadas em momentos distintos, eventuais relações entre essas tabelas não serão criadas e deverão ser criadas manualmente. Se nenhuma relação aparecer, significa que não há nenhuma relação na fonte de dados. Você pode criá-los manualmente no modelo de dados.

### <a name="take-a-closer-look"></a>Uma visão mais detalhada

No modo de exibição de diagrama, observe uma seta, um asterisco e um número de linhas que mostram a relação entre tabelas.

![as-lesson4-line](../tutorial-tabular-1400/media/as-lesson4-line.png)

A seta mostra a direção do filtro. O asterisco mostra essa tabela é o *muitos* lado na cardinalidade da relação e a outra mostra essa tabela é a *um* lado da relação. Se você precisar editar uma relação; Por exemplo, alterar a direção da relação do filtro ou cardinalidade, clique duas vezes na linha da relação para abrir a caixa de diálogo Editar relação.

![as-lesson4-edit](../tutorial-tabular-1400/media/as-lesson4-edit.png)

Esses recursos são destinados a modelagem de dados avançada e estão fora do escopo deste tutorial. Para obter mais informações, consulte [bidirecional entre os filtros para modelos tabulares no Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

Em alguns casos, talvez seja necessário criar relações adicionais entre tabelas no modelo para oferecer suporte a uma lógica corporativa específica. Para este tutorial, você precisa criar três relações adicionais entre as tabelas FactInternetSales e a tabela DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Para adicionar novas relações entre tabelas  
  
1.  No designer de modelo, no **FactInternetSales** de tabela, clique e segure na **OrderDate** coluna, em seguida, arraste o cursor para o **data** coluna no  **DimDate** tabela e, em seguida, solte.  

    Uma linha sólida aparece, indicando que você criou uma relação ativa entre a **OrderDate** coluna o **vendas pela Internet** tabela e o **data** coluna o  **Data** tabela. 
  
      ![as-lesson4-new](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > Ao criar relações, a direção de cardinalidade e de filtragem entre a tabela primária e a tabela de pesquisa relacionada é selecionada automaticamente.  
  
2.  No **FactInternetSales** , clique e mantenha pressionado na **DueDate** coluna, em seguida, arraste o cursor para o **data** coluna no **DimDate** tabela e, em seguida, solte.  
  
    Uma linha pontilhada aparece, indicando que você criou uma relação inativa entre a **DueDate** coluna o **FactInternetSales** tabela e o **data** coluna o  **DimDate** tabela. Você pode ter várias relações entre tabelas, mas só uma relação pode estar ativa por vez. Relações inativas podem ficar ativas para executar agregações especiais em expressões do DAX personalizadas.  
  
3.  Por fim, crie mais uma relação. No **FactInternetSales** , clique e mantenha pressionado na **ShipDate** coluna, em seguida, arraste o cursor para o **data** coluna no **DimDate** tabela e, em seguida, solte.  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 5: Criar colunas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).
  
  
  
