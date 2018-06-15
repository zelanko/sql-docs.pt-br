---
title: Compilando medidas em MDX | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2095d3bde254a59c5b2edbe8ebb117854ab7777
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026093"
---
# <a name="mdx-building-measures"></a>Medidas de construção de MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Nas expressões MDX, uma medida é uma expressão DAX nomeada que é resolvida pelo cálculo da expressão para retornar um valor em um Modelo de Tabela. Essa simples definição abrange uma quantidade enorme implicações. A capacidade de construir e usar medidas em uma consulta MDX proporciona uma grande capacidade de manipulação de dados de tabela.  
  
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
 [Criar declaração de membro & #40; MDX & #41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Referência de função MDX & #40; MDX & #41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Instrução SELECT & #40; MDX & #41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
