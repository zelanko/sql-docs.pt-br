---
title: Elemento DefaultDetails (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6d64d654ba9bd863c5497bb3c38864c641d7573d
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="defaultdetails-element-csdlbi"></a>Elemento DefaultDetails (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento DefaultDetails representa uma lista de referências de propriedade que juntas definem o "conjunto de campos padrão" de colunas na tabela. Cada propriedade pode fazer referência apenas a uma medida ou uma coluna.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento DefaultDetails.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|DefaultDetailsPosition|Não|Um número inteiro positivo que indica presença e posição na coleção.|  
  
## <a name="example"></a>Exemplo  
 **Tabela**  
  
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
  
  
