---
title: Tuplas | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 35b629ae-b1ef-44b1-b556-96956aeb56e7
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4720db7c001c17a99016e9d81b32ee46d990e06f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="tuples"></a>Tuplas
  Uma tupla identifica exclusivamente uma fatia de dados de um cubo. A tupla é formada por uma combinação de membros de dimensão, contanto que não haja dois ou mais membros pertencentes à mesma hierarquia.  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>Membros de atributo implícitos ou padrão em uma tupla  
 Ao definir uma tupla em uma consulta ou expressão MDX, você não precisa explicitamente incluir o membro de atributo de cada hierarquia de atributo. Se um membro de uma hierarquia de atributo não for explicitamente incluído em uma consulta ou em uma expressão, o membro padrão para aquela hierarquia de atributo será o membro de atributo implicitamente incluso na tupla. Salvo indicação contrária explicitamente definida em um cubo, o membro padrão para cada hierarquia de atributo é o membro (All), se houver um membro (All). Se não houver um membro (All) em uma hierarquia de atributo, o membro padrão será um membro do nível superior da hierarquia de atributo. A medida padrão é a primeira medida especificada no cubo, salvo se uma medida padrão estiver explicitamente definida. Para obter mais informações, consulte [Definir um membro padrão](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md) e [DefaultMember &#40;MDX&#41;](../../../mdx/defaultmember-mdx.md).  
  
 Por exemplo, a tupla a seguir identifica uma célula única no banco de dados do Adventure Works, definindo explicitamente um membro único da dimensão Medidas.  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 O exemplo anterior identifica exclusivamente a célula que consiste no membro Valor das Vendas do Revendedor da dimensão Medidas e o membro padrão de cada hierarquia de atributo no cubo. O membro padrão é o membro (All) para cada hierarquia de atributo diferente da hierarquia de atributo Moeda de Destino. O membro padrão da hierarquia Moeda de Destino é o membro Dólar (EUA) (esse membro padrão está definido no script MDX no cubo Adventure Works).  
  
> [!IMPORTANT]  
>  O membro de uma hierarquia de atributo em uma tupla também é afetado por relações definidas entre atributos dentro de uma dimensão.  
  
 A consulta a seguir retorna o valor da célula referenciada pela tupla especificada no exemplo anterior ($80.450.596,98).  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Quando você especifica um eixo para um conjunto (nesse caso, composto por uma tupla única) em uma consulta, você deve começar especificando um conjunto para o eixo da coluna antes de especificar um conjunto para o eixo de linhas. O eixo da coluna também pode ser referido como *eixo (0)* ou simplesmente *0*. Para obter mais informações sobre consultas MDX, consulte [A consulta MDX básica &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md).  
  
### <a name="tuples-as-values-or-member-references"></a>Tuplas como valores ou referências de membro  
 Você pode usar uma tupla em uma consulta para retornar o valor na célula que é referenciado pela tupla, como no exemplo anterior. Ou você pode usar uma tupla em uma expressão para explicitamente se referir aos membros especificados na tupla. A consulta ou a expressão podem utilizar funções que retornam ou consomem tuplas. Uma tupla pode ser usada para se referir ao valor da célula que a tupla especifica, ou especificar uma combinação de membros, quando utilizada em uma função.  
  
### <a name="tuple-dimensionality"></a>Dimensionalidade de tupla  
 A *dimensionalidade* de uma tupla se refere à sequência ou ordem dos membros na tupla. Como os membros implícitos sempre ocorrem na mesma ordem, na maioria das vezes a dimensionalidade é considerada em termos dos membros explicitamente definidos da tupla. A ordenação dos membros da tupla é importante quando você define um conjunto de tuplas. O exemplo a seguir inclui dois membros em uma tupla no eixo da coluna.  
  
```  
SELECT   
([Measures].[Reseller Sales Amount],[Date].[Calendar Year].[CY 2004]) ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Quando você especificar explicitamente um membro em uma tupla de mais de uma dimensão, você deve incluir toda a tupla entre parênteses. Ao especificar somente um membro único em uma tupla, os parênteses são opcionais.  
  
 A tupla na consulta no exemplo anterior especifica o retorno da célula do cubo na interseção da Medida do Valor das Vendas do Revendedor da dimensão Medidas e o membro CY 2004 da hierarquia de atributo Ano Civil na dimensão Data.  
  
> [!NOTE]  
>  Um membro de atributo pode ser referido por seu nome de membro ou sua chave de membro. No exemplo anterior, você poderia substituir a referência [CY 2004] por &[2004].  
  
## <a name="see-also"></a>Consulte também  
 [Principais conceitos em MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Cube Space](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Trabalhando com membros, tuplas e conjuntos de &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)  
  
  
