---
title: Elemento DisplayKey (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 01c6272e3007202bae4f3f2f595579fc095ddc5a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040184"
---
# <a name="displaykey-element-csdlbi"></a>Elemento DisplayKey (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento DisplayKey contém uma lista dos elementos a seguir que juntos constituem um identificador forte. O DisplayKey é encontrado apenas como um filho do elemento EntityType. Ele pode fazer referência a colunas ou extremidades de função.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os atributos do elemento DisplayKey.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|IsDisplayKey|Não|Verdadeiro ou falso.|  
  
## <a name="remarks"></a>Comentários  
 Este elemento é para relatórios. O elemento ao qual você aplica esse atributo não precisa ser a chave de tabela real, apenas um elemento que será apresentado como a chave. No entanto, a coluna que você usa para o DisplayKey deve conter valores exclusivos.  
  
## <a name="example"></a>Exemplo  
 **Tabela**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra uma coluna no exemplo de modelo de dados da AdventureWorks que foi designada como o DisplayKey da tabela.  
  
```  
<sample in progress>  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um trecho da representação do cubo Operações da Contoso. Nesse modelo, a coluna Color foi marcada como a chave de exibição da tabela Bikes.  
  
```  
  
<EntityType   
    Name="Bike">  
.. .. ..  
<Property   
    Name="Color"   
    Type="String"   
    MaxLength="Max"   
    Unicode="true"   
    FixedLength="false">  
<bi:Property   
    ContextualNameRule="Context"   
    Alignment="Left" Units="counts"   
    SortDirection="Descending"   
    IsRightToLeft="true"   
    DefaultAggregateFunction="Max" />  
</Property>  
.. .. ..  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>>  
.. .. ..  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o modelo de objeto de tabela em compatibilidade 1050 1103 por meio de níveis](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceitos da CSDLBI](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  
