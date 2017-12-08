---
title: Elemento Members (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Members Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords: Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2d2b4f8a9c466fa85bdd1131a58c2c11fc232967
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="members-element-xmla"></a>Elemento Members (XMLA)
  Contém uma coleção de [membro](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) elementos contidos pelo pai [CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md) elemento.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)|  
|Elementos filho|[Membro](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|Hierarquia|Atributo **String** obrigatório. O nome da hierarquia à qual os membros contidos pelo **membros** elemento pertence.|  
  
## <a name="remarks"></a>Comentários  
 Quando um aplicativo cliente define o **AxisFormat** propriedade *ClusterFormat*, os membros em cada eixo são divididos em clusters nos quais cada cluster representa um produto cruzado entre conjuntos ordenados de membros de cada hierarquia. Cada **eixo** elemento consiste em um ou mais **CrossProduct** elementos. Cada **CrossProduct** elemento contém um **membros** elemento para cada hierarquia no eixo. O **membros** elemento, por sua vez, contém um **membro** elemento para cada membro da hierarquia especificada incluída no produto cruzado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra a estrutura do **membros** elemento quando um cliente especifica *ClusterFormat* para o **AxisFormat** propriedade XMLA, considerando o membros a seguir para o eixo:  
  
||||||  
|-|-|-|-|-|  
|Hierarquia de **tempo**|1999|1999|2000|2001|  
|Hierarquia de **categoria**|Real|Orçamento|Orçamento|Orçamento|  
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
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
