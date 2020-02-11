---
title: Especificando o conteúdo de um eixo de segmentação (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slicer axis
- filtering data [MDX]
ms.assetid: c56b0a70-cdec-427f-990e-425290344e7d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12e2d2f543694a1da418f5e8eb4b900eaa123d97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074057"
---
# <a name="specifying-the-contents-of-a-slicer-axis-mdx"></a>Especificando o conteúdo de um eixo do slicer (MDX)
  O eixo de slicer filtra os dados retornados pela instrução MDX SELECT, restringindo os dados retornados para que somente os dados da intersecção com os membros especificados sejam retornados. Pode ser considerado como um eixo adicional invisível em uma consulta. O eixo de slicer é definido na cláusula WHERE da instrução MDX SELECT.  
  
## <a name="slicer-axis-syntax"></a>Sintaxe de eixo de slicer  
 Para especificar um eixo de slicer explicitamente, use a `<SELECT slicer axis clause>` no formato MDX, como descrita na sintaxe a seguir:  
  
```  
<SELECT slicer axis clause> ::=  WHERE Set_Expression  
```  
  
 Na sintaxe do eixo de slicer mostrada, `Set_Expression` pode assumir a expressão de tupla, que é tratada como um conjunto para a avaliação ou como uma expressão de conjunto. Se for especificada uma expressão de conjunto, a linguagem MDX tentará avaliar o conjunto, agregando as células de resultado a cada tupla do conjunto. Em outras palavras, a linguagem MDX tentará usar a função [Aggregate](/sql/mdx/aggregate-mdx) no conjunto, agregando cada medida pela sua função de agregação associada. Além disso, se a expressão de conjunto não puder ser expressa como uma interjunção dos membros da hierarquia do atributo, a linguagem MDX tratará as células que ficarem fora da expressão de conjunto do slicer como nulas para a avaliação.  
  
> [!IMPORTANT]  
>  Diferente da cláusula WHERE no SQL, a cláusula WHERE em uma instrução MDX SELECT nunca filtra diretamente o que é retornado no eixo Linhas de uma consulta. Para filtrar o que aparece no eixo Linhas ou Colunas de uma consulta, você pode usar diversas funções MDX, como, por exemplo, FILTER, NONEMPTY e TOPCOUNT.  
  
### <a name="implicit-slicer-axis"></a>Eixo de slicer implícito  
 Se um membro de uma hierarquia do cubo não for explicitamente incluído em um eixo de consulta, o membro padrão dessa hierarquia será incluído implicitamente no eixo de slicer. Para obter mais informações sobre membros padrão, consulte [Definir um membro padrão](../attribute-properties-define-a-default-member.md).  
  
## <a name="examples"></a>Exemplos  
 A seguinte consulta não inclui uma cláusula WHERE e retorna o valor da medida Quantidade de Vendas pela Internet todos os Anos Civis:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
 Veja como adicionar uma cláusula WHERE:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States])  
  
```  
  
 não altera o que é retornado em Linhas ou Colunas na consulta; altera os valores retornados para cada célula. Neste exemplo, a consulta é fatiada de forma que isso retorne o valor de Quantidade de Vendas pela Internet durante todos os Anos Civis, mas só para Clientes que moram nos Estados Unidos. Vários membros de hierarquias diferentes podem ser acrescentados à cláusula WHERE. A seguinte consulta mostra o valor de Quantidade de Vendas pela Internet durante todos os Anos Civis para Clientes que moram nos Estados Unidos e que compraram Produtos na Categoria Bicicletas:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States], [Product].[Category].&[1])  
```  
  
 Se você desejar usar vários membros da mesma hierarquia, precisará incluir um conjunto na cláusula WHERE. Por exemplo, a seguinte consulta mostra o valor da Quantidade de Vendas pela Internet durante todos os Anos Civis para Clientes que compraram Produtos na Categoria Bicicletas e moram nos Estados Unidos ou no Reino Unido:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE(  
{[Customer].[Customer Geography].[Country].&[United States]  
, [Customer].[Customer Geography].[Country].&[United Kingdom]}  
, [Product].[Category].&[1])  
  
```  
  
 Como mencionado antes, o uso de um conjunto na cláusula WHERE implicitamente agregará valores a todos os membros do conjunto. Nesse caso, a consulta mostra valores agregados para os Estados Unidos e o Reino Unido em cada célula.  
  
  
