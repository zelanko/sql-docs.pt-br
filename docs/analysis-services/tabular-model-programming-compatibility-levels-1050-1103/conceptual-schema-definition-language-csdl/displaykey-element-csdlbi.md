---
title: Elemento DisplayKey (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 7d881278-1e77-42e1-8cfc-f1bbd9ec2340
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 10f388c46f9d79314107eb375aa4de6dacdf4fbf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="displaykey-element-csdlbi"></a>Elemento DisplayKey (CSDLBI)
  O elemento DisplayKey contém uma lista dos elementos a seguir que juntos constituem um identificador forte. O DisplayKey é encontrado apenas como um filho do elemento EntityType. Ele pode fazer referência a colunas ou extremidades de função.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os atributos do elemento DisplayKey.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|IsDisplayKey|Não|Verdadeiro ou falso.|  
  
## <a name="remarks"></a>Comentários  
 Este elemento é para relatórios. O elemento ao qual você aplica esse atributo não precisa ser a chave de tabela real, apenas um elemento que será apresentado como a chave. No entanto, a coluna que você usa para o DisplayKey deve conter valores exclusivos.  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
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
  
  
