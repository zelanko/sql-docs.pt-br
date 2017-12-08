---
title: Elemento DefaultDetails (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 05a08baa-23cc-4011-9c2e-f60a20bb87da
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 25dafd209e16e820c6e0a70acb268d5c5d724f70
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="defaultdetails-element-csdlbi"></a>Elemento DefaultDetails (CSDLBI)
  O elemento DefaultDetails representa uma lista de referências de propriedade que juntas definem o "conjunto de campos padrão" de colunas na tabela. Cada propriedade pode fazer referência apenas a uma medida ou uma coluna.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento DefaultDetails.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|DefaultDetailsPosition|Não|Um número inteiro positivo que indica presença e posição na coleção.|  
  
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
 [Noções básicas sobre o modelo de objeto de tabela em compatibilidade 1050 1103 por meio de níveis](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceitos da CSDLBI](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  
