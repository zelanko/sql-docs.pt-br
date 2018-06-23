---
title: Elemento Axis (XMLA) | Microsoft Docs
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
- Axis Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: e30ff03b6e1a58a079d35f8e846ed176c42a3a31
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020094"
---
# <a name="axis-element-xmla"></a>Elemento Axis (XMLA)
  Contém um conjunto de tuplas utilizado para representar um único eixo em um conjunto de dados multidimensional contido por um [eixos](axes-element-xmla.md) elemento que usa o [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) retornado pelo tipo de dados, o [Execute](../xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Axes>  
   ...  
   <Axis> <!-- when AxisFormat XMLA property is set to ClusterFormat -->  
      <CrossProduct>...</CrossProduct>  
   </Axis>  
   <Axis> <!-- when AxisFormat XMLA property is set to TupleFormat or CustomFormat -->  
      <Tuples>...</Tuples>  
   </Axis>  
   ...  
</Axes>  
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
|Elementos pai|[Eixos](axes-element-xmla.md)|  
|Elementos filho|[CrossProduct](crossproduct-element-xmla.md) ou [tuplas](tuples-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O conteúdo do elemento `Axis` varia dependendo do valor da propriedade XMLA `AxisFormat` utilizada pelo método `Execute`.  
  
## <a name="tupleformat"></a>TupleFormat  
 Quando um aplicativo cliente define o `AxisFormat` propriedade *TupleFormat*, um eixo é representado como um conjunto de tuplas. Cada elemento `Axis` contém um elemento `Tuples` que representa o conjunto de tuplas naquele eixo. Cada tupla é representada usando um elemento `Tuple` que contém elementos `Member` de toda hierarquia no eixo.  
  
## <a name="clusterformat"></a>ClusterFormat  
 Quando um aplicativo cliente define o `AxisFormat` propriedade *ClusterFormat*, os membros em cada eixo são divididos em clusters nos quais cada cluster representa um produto cruzado entre conjuntos ordenados de membros de cada hierarquia. Cada elemento `Axis` consiste em um ou mais elementos `CrossProduct`. Cada elemento `CrossProduct` contém um elemento `Members` para cada hierarquia no eixo.  
  
## <a name="customformat"></a>CustomFormat  
 Quando um aplicativo cliente define o `AxisFormat` propriedade *CustomFormat*, o valor será tratado o mesmo que o *TupleFormat* valor por uma instância do Analysis Services.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo a seguir ilustra a estrutura do `Axis` elementos quando um cliente especifica *TupleFormat* ou *CustomFormat* para o `AxisFormat` propriedade XMLA, considerando o seguinte membros do eixo:  
  
|||||  
|-|-|-|-|  
|Hierarquia de `Time`|1999|1999|2000|  
|Hierarquia de `Category`|Real|Orçamento|Orçamento|  
  
### <a name="code"></a>Código  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <Tuples>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
      </Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
### <a name="description"></a>Description  
 O exemplo a seguir ilustra a estrutura do `Axis` elementos quando um cliente especifica *ClusterFormat* para o `AxisFormat` propriedade XMLA, fornecida aos seguintes membros do eixo:  
  
||||||  
|-|-|-|-|-|  
|Hierarquia de `Time`|1999|1999|2000|2001|  
|Hierarquia de `Category`|Real|Orçamento|Orçamento|Orçamento|  
|Clusters|Cluster 1|Cluster 1|Cluster 1|Cluster 2|  
  
### <a name="code"></a>Código  
  
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
  
  