---
title: Elemento MemberRef (CSDLBI) | Microsoft Docs
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
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
caps.latest.revision: 4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f308a9c890c36b5948c0f2c8a8468350c2e7cf4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265259"
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
  
  
