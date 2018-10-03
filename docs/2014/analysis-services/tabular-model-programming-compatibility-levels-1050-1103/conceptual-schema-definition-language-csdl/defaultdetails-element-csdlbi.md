---
title: Elemento DefaultDetails (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 05a08baa-23cc-4011-9c2e-f60a20bb87da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa1fcc05363cf356d5895c0d5e6f62c037f45fb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120856"
---
# <a name="defaultdetails-element-csdlbi"></a>Elemento DefaultDetails (CSDLBI)
  O elemento DefaultDetails representa uma lista de referências de propriedade que juntas definem o "conjunto de campos padrão" de colunas na tabela. Cada propriedade pode fazer referência apenas a uma medida ou uma coluna.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento DefaultDetails.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|DefaultDetailsPosition|não|Um número inteiro positivo que indica presença e posição na coleção.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um trecho do exemplo de modelo de dados da AdventureWorks. Há apenas um conjunto de colunas padrão para a tabela Employees (Title). No entanto, três colunas foram definidas como conjunto de campos padrão para a tabela Products.  
  
```  
  
<EntityType   
    Name="DimEmployee">  
....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Title" />  
   </bi:DefaultDetails>  
.....  
<EntityType   
    Name="Products">  
.....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
      <bi:MemberRef Name="DealerPrice" />  
      <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, mostra um trecho da definição da tabela Bike no cubo Operações da Contoso. Essa anotação indica que a coluna Color deverá ser exibida por padrão se nenhuma outra coluna de exibição for especificada.  
  
```  
  
<EntityType Name="Bike">  
   <Key>  
   <PropertyRef Name="RowNumber" />  
   </Key>  
....  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
   </bi:DefaultDetails>  
   <bi:SortMembers>  
      <bi:MemberRef Name="Color" />  
   </bi:SortMembers>  
....  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o modelo de objeto Tabular](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceitos da CSDLBI](../csdlbi-concepts.md)  
  
  
