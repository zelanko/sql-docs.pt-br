---
title: Elemento DisplayKey (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 7d881278-1e77-42e1-8cfc-f1bbd9ec2340
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 907bb04d59225180fad91b63971d578181c6663d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019440"
---
# <a name="displaykey-element-csdlbi"></a>Elemento DisplayKey (CSDLBI)
  O elemento DisplayKey contém uma lista dos elementos a seguir que juntos constituem um identificador forte. O DisplayKey é encontrado apenas como um filho do elemento EntityType. Ele pode fazer referência a colunas ou extremidades de função.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os atributos do elemento DisplayKey.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|IsDisplayKey|não|Verdadeiro ou falso.|  
  
## <a name="remarks"></a>Remarks  
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
 [Noções básicas sobre o modelo de objeto de tabela](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceitos da CSDLBI](../csdlbi-concepts.md)  
  
  