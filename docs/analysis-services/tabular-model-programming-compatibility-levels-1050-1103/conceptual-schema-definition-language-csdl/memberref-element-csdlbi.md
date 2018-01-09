---
title: Elemento MemberRef (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8c1bb47c2273d79e320e53b49c524112b067a2d3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="memberref-element-csdlbi"></a>Elemento MemberRef (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]O elemento MemberRef identifica o nome de uma propriedade que é o destino de uma referência.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento MemberRef.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Nome|Sim|O nome da propriedade contida em um elemento MemberRef.|  
  
## <a name="memberrefs-element"></a>Elemento MemberRefs  
 MemberRefs é um tipo complexo que define uma coleção de membros em que cada membro é contido em um elemento MemberRef.  
  
 A tabela a seguir lista os elementos e atributos do tipo MemberRefs.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|MemberRef|Sim|Uma cadeia de caracteres que contém a referência do membro.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, representa uma parte do exemplo do modelo de dados da AdventureWorks que define a tabela Products. Aqui, o elemento MemberRef é usado para cada coluna que é incluída no conjunto de campos padrão do modelo.  
  
```  
  
<bi:EntityType>  
   <bi:DefaultDetails>  
     <bi:MemberRef Name="Color" />  
     <bi:MemberRef Name="DealerPrice" />  
     <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir, na versão 1.1 da CSDLBI, representa uma parte do cubo Operações da Contoso que define a tabela Bikes. Nesse exemplo, um elemento MemberRef é usado para especificar o nome da coluna usada como o conjunto de campos padrão em relatórios e outro elemento MemberRef é usado para fazer referência à coluna que fornece a ordem de classificação.  
  
```  
  
<bi:DefaultDetails>  
   <bi:MemberRef Name="Color" />  
</bi:DefaultDetails>  
  
<bi:SortMembers>  
   <bi:MemberRef Name="Color" />  
</bi:SortMembers>  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica para Anotações de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
