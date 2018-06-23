---
title: Elemento Members (XMLA) | Microsoft Docs
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
api_name:
- Members Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords:
- Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5d812d0eea48c4f2b54352f61a176462b280071a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116224"
---
# <a name="members-element-xmla"></a>Elemento Members (XMLA)
  Contém uma coleção de [membro](member-element-xmla.md) elementos contidos pelo pai [CrossProduct](crossproduct-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CrossProduct>  
   <Members Hierarchy="string">  
      <Member>...</Member>  
   </Members>  
   ...  
</CrossProduct>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CrossProduct](crossproduct-element-xmla.md)|  
|Elementos filho|[Membro](member-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|Hierarquia|Necessário `String` atributo. O nome da hierarquia à qual os membros contidos pelo elemento `Members` pertencem.|  
  
## <a name="remarks"></a>Remarks  
 Quando um aplicativo cliente define o `AxisFormat` propriedade *ClusterFormat*, os membros em cada eixo são divididos em clusters nos quais cada cluster representa um produto cruzado entre conjuntos ordenados de membros de cada hierarquia. Cada elemento `Axis` consiste em um ou mais elementos `CrossProduct`. Cada elemento `CrossProduct` contém um elemento `Members` para cada hierarquia no eixo. O elemento `Members`, por sua vez, contém um elemento `Member` para cada membro da hierarquia especificada incluída no produto cruzado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra a estrutura do `Members` elemento quando um cliente especifica *ClusterFormat* para o `AxisFormat` propriedade XMLA, fornecida aos seguintes membros do eixo:  
  
||||||  
|-|-|-|-|-|  
|Hierarquia de `Time`|1999|1999|2000|2001|  
|Hierarquia de `Category`|Real|Orçamento|Orçamento|Orçamento|  
|Clusters|Cluster 1|Cluster 1|Cluster 1|Cluster 2|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size = "4">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
      <CrossProduct Size = "1">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[2001]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  