---
title: Elemento MemberRef (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 79b6f2684dabcb45cfddac626bc2a6aa140298f3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="memberref-element-csdlbi"></a>Elemento MemberRef (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento MemberRef identifica o nome de uma propriedade que é o destino de uma referência.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento MemberRef.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|Nome|Sim|O nome da propriedade contida em um elemento MemberRef.|  
  
## <a name="memberrefs-element"></a>Elemento MemberRefs  
 MemberRefs é um tipo complexo que define uma coleção de membros em que cada membro é contido em um elemento MemberRef.  
  
 A tabela a seguir lista os elementos e atributos do tipo MemberRefs.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|MemberRef|Sim|Uma cadeia de caracteres que contém a referência do membro.|  
  
## <a name="example"></a>Exemplo  
 **Tabela**  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica para anotações de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
