---
title: Elemento CrossProduct (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CrossProduct Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CrossProduct
- microsoft.xml.analysis.crossproduct
- urn:schemas-microsoft-com:xml-analysis#CrossProduct
helpviewer_keywords:
- CrossProduct element
ms.assetid: a9a1584e-d2dd-45db-a918-d694c20d8189
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0d76cc463d39a3b33de41f1c342f5d9f8f800bb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278204"
---
# <a name="crossproduct-element-xmla"></a>Elemento CrossProduct (XMLA)
  Contém um produto cruzado entre conjuntos ordenados de membros de cada hierarquia para um [eixo](axis-element-xmla.md) elemento que usa o [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) retornado por tipo de dados, o [Execute](../xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Axis>  
   ...  
   <CrossProduct Size="integer">  
      <Members>...</Members>  
   </CrossProduct>  
   ...  
</Axis>  
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
|Elementos pai|[Axis](axis-element-xmla.md)|  
|Elementos filho|[Membros](members-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|Tamanho|Necessário `Integer` atributo. Indica o número de tuplas contido no produto cruzado representado pelo elemento `CrossProduct`.|  
  
## <a name="remarks"></a>Remarks  
 Quando um aplicativo cliente definir a `AxisFormat` propriedade para *ClusterFormat*, os membros em cada eixo são divididos em clusters em que cada cluster representa um produto cruzado entre conjuntos ordenados de membros de cada hierarquia. Cada cluster é representado por um elemento `CrossProduct` . Cada elemento `CrossProduct` contém um elemento `Members` para cada hierarquia no eixo. Um elemento `CrossProduct` pode conter membros de uma única hierarquia.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra a estrutura do `CrossProduct` elemento quando um cliente especifica *ClusterFormat* para o `AxisFormat` propriedade XMLA, fornecida aos seguintes membros do eixo:  
  
||||||  
|-|-|-|-|-|  
|Hierarquia de `Time`|1999|1999|2000|2001|  
|Hierarquia de `Category`|Real|Orçamento|Orçamento|Orçamento|  
|Clusters|Cluster 1|Cluster 1|Cluster 1|Cluster 2|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size="4">  
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
      <CrossProduct Size="1">  
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
  
  
