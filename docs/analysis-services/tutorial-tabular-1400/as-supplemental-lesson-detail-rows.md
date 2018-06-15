---
title: 'A lição suplementar tutorial do Analysis Services: linhas de detalhes | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0518cdd7707c5973bfd055af997a75c9b67d7479
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045740"
---
# <a name="supplemental-lesson---detail-rows"></a>Lição suplementar - linhas de detalhes

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição suplementar, você pode usar o Editor do DAX para definir uma expressão personalizada de linhas de detalhes. Uma expressão de linhas de detalhes é uma propriedade em uma medida, proporcionando aos usuários finais para obter mais informações sobre os resultados agregados de uma medida. 
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo lição suplementar faz parte de um tutorial de modelagem de tabela. Antes de executar as tarefas nesta lição suplementar, você deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet Sales concluído.  
  
## <a name="whats-the-issue"></a>O que é o problema?

Vamos examinar os detalhes da medida InternetTotalSales, antes de adicionar uma expressão de linhas de detalhes.

1.  No SSDT, clique no **modelo** menu > **analisar no Excel** para abrir o Excel e criar uma tabela dinâmica em branco.
  
2.  Em **PivotTable Fields**, adicione o **InternetTotalSales** medidas da tabela FactInternetSales para **valores**, **CalendarYear** da tabela DimDate para **colunas**, e **EnglishCountryRegionName** para **linhas**. A tabela dinâmica agora oferece um resultados agregados da medida InternetTotalSales regiões e ano. 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. Na tabela dinâmica, clique duas vezes em um valor agregado para um ano e um nome de região. Aqui é clicado duas vezes o valor para a Austrália e o ano de 2014. Uma nova planilha é aberta que contém dados, mas os dados não são úteis.

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
O que queremos ver aqui é uma tabela que contém colunas e linhas de dados que contribuem para o resultado agregado da medida InternetTotalSales. Para fazer isso, é possível adicionar uma expressão de linhas de detalhes como uma propriedade da medida.

## <a name="add-a-detail-rows-expression"></a>Adicionar uma expressão de linhas de detalhes

#### <a name="to-create-a-detail-rows-expression"></a>Para criar uma expressão de linhas de detalhes 
  
1. Na grade de medida da tabela FactInternetSales, clique o **InternetTotalSales** medidas. 

2. Em **propriedades** > **expressão de linhas de detalhes**, clique no botão do editor para abrir o Editor DAX.

    ![as-lesson-detail-rows-ellipse](../tutorial-tabular-1400/media/as-lesson-detail-rows-ellipse.png)

3. No Editor do DAX, digite a expressão a seguir:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Essa expressão especifica nomes de colunas, e os resultados de medidas da tabela FactInternetSales e tabelas relacionadas são retornados quando um usuário clica duas vezes em um resultado agregado em uma tabela dinâmica ou relatório.

4. Novamente no Excel, excluir a planilha criada na etapa 3, em seguida, clique duas vezes em um valor agregado. Neste momento, com uma propriedade de expressão de linhas de detalhe definida para a medida, uma nova planilha é aberta que contém dados muito mais útil.

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. Reimplante o modelo.

  
## <a name="see-also"></a>Consulte também  

[Função SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[Lição suplementar - Segurança dinâmica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lição suplementar - Hierarquias desbalanceadas](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
