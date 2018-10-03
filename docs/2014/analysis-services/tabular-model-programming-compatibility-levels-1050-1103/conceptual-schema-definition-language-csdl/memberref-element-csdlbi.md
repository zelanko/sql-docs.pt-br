---
title: Elemento MemberRef (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb0912afd99c7a4859ca4750a3ba1b66fdecd5f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205706"
---
# <a name="memberref-element-csdlbi"></a>Elemento MemberRef (CSDLBI)
  O elemento MemberRef identifica o nome de uma propriedade que é o destino de uma referência.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica para Anotações de BI para CSDL](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
