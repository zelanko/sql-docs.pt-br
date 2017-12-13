---
title: Compilando medidas em MDX | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f0347835-4983-4d26-acbb-6c8fae7992bd
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5d1e4e637d3cee754573c2d59776d7241c89d2bf
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-building-measures"></a>Medidas de construção de MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Em expressões multidimensionais (MDX), uma medida é uma expressão DAX nomeada que é resolvida pelo cálculo da expressão para retornar um valor em um modelo de tabela. Essa simples definição abrange uma quantidade enorme implicações. A capacidade de construir e usar medidas em uma consulta MDX proporciona uma grande capacidade de manipulação de dados de tabela.  
  
> [!WARNING]  
>  As medidas podem ser definidas apenas em modelos de tabela; se o seu banco de dados estiver definido no modo multidimensional, a criação de uma medida gerará um erro  
  
 Para criar uma medida que seja definida como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Em seguida, você pode usar a medida em uma instrução MDX SELECT. Usando essa abordagem, o membro calculado criado pelo uso da palavra-chave pode ser alterado sem afetar a instrução SELECT. No entanto, em MDX você referencia a medida de uma forma diferente da adotada nas expressões DAX; para referenciar a medida você a denomina como membro da dimensão [Measures], consulte o seguinte exemplo de MDX:  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 Isso retornará os dados seguintes quando executado:  
  
||Total Sales Amount||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>Consulte também  
 [Instrução CREATE MEMBER &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Instrução SELECT &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
