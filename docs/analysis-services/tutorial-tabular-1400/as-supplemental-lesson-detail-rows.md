---
title: 'Analysis Services lição suplementar de tutorial: Linhas de detalhes | Microsoft Docs'
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
ms.openlocfilehash: bad45d18c351e838ec944b1ae67e3ce88c7e1d20
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263310"
---
# <a name="supplemental-lesson---detail-rows"></a>Lição suplementar – Linhas de detalhes

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição suplementar, você pode usar o Editor do DAX para definir uma expressão de linhas de detalhes personalizada. Uma expressão de linhas de detalhes é uma propriedade em uma medida, fornecendo aos usuários finais a obter mais informações sobre os resultados agregados de uma medida. 
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo de lição suplementar faz parte de um tutorial de modelagem de tabela. Antes de executar as tarefas nesta lição suplementar, você deve ter concluído todas as lições anteriores ou ter um projeto de modelo de exemplo Adventure Works Internet Sales concluído.  
  
## <a name="whats-the-issue"></a>O que é o problema?

Vamos examinar os detalhes da medida InternetTotalSales, antes de adicionar uma expressão de linhas de detalhes.

1.  No SSDT, clique o **modelo** menu > **analisar no Excel** para abrir o Excel e criar uma tabela dinâmica em branco.
  
2.  Na **PivotTable Fields**, adicione o **InternetTotalSales** medida da tabela FactInternetSales a **valores**, **CalendarYear** de a tabela DimDate **colunas**, e **EnglishCountryRegionName** para **linhas**. A tabela dinâmica agora fornece um resultado agregado da medida InternetTotalSales por regiões e ano. 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. Na tabela dinâmica, clique duas vezes em um valor agregado para um ano e um nome de região. Aqui, clicamos duas vezes o valor para Austrália e o ano de 2014. Uma nova folha será aberta contendo dados, mas não os dados úteis.

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
O que queremos ver aqui é uma tabela contendo colunas e linhas de dados que contribuem para o resultado agregado da medida InternetTotalSales. Para fazer isso, podemos adicionar uma expressão de linhas de detalhes como uma propriedade da medida.

## <a name="add-a-detail-rows-expression"></a>Adicionar uma expressão de linhas de detalhes

#### <a name="to-create-a-detail-rows-expression"></a>Para criar uma expressão de linhas de detalhes 
  
1. Na grade de medida da tabela FactInternetSales, clique o **InternetTotalSales** medidas. 

2. Na **propriedades** > **expressão de linhas de detalhes**, clique no botão do editor para abrir o Editor do DAX.

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

4. No Excel, exclua a planilha criada na etapa 3 e, em seguida, clique duas vezes em um valor agregado. Neste momento, com uma propriedade de expressão de linhas de detalhes definida para a medida, uma nova folha será aberta contendo dados muito mais úteis.

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. Reimplante o modelo.

  
## <a name="see-also"></a>Confira também  

[Função SELECTCOLUMNS (DAX)](/dax/selectcolumns-function-dax)  
[Lição suplementar - Segurança dinâmica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lição suplementar - Hierarquias desbalanceadas](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
