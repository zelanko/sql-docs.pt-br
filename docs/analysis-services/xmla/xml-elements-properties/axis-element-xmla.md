---
title: Elemento Axis (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Axis Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 136ce9c4b39d0b9a93abc491850b63783ff4bf1c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="axis-element-xmla"></a>Elemento Axis (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém um conjunto de tuplas utilizado para representar um único eixo em um conjunto de dados multidimensional contido por um [eixos](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md) elemento que usa o [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) retornado pelo tipo de dados, o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Eixos](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)|  
|Elementos filho|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md) ou [tuplas](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O conteúdo do **eixo** elemento varia dependendo do valor da **AxisFormat** propriedade XMLA usada pelo **Execute** método.  
  
## <a name="tupleformat"></a>TupleFormat  
 Quando um aplicativo cliente definir a propriedade **AxisFormat** como *TupleFormat*, um eixo é representado como um conjunto de tuplas. Cada **eixo** elemento contém um **tuplas** elemento que representa o conjunto de tuplas naquele eixo. Cada tupla é representada usando um elemento **Tuple** que contém elementos **Member** de toda hierarquia no eixo.  
  
## <a name="clusterformat"></a>ClusterFormat  
 Quando um aplicativo cliente define o **AxisFormat** propriedade *ClusterFormat*, os membros em cada eixo são divididos em clusters nos quais cada cluster representa um produto cruzado entre conjuntos ordenados de membros de cada hierarquia. Cada **eixo** elemento consiste em um ou mais **CrossProduct** elementos. Cada **CrossProduct** elemento contém um **membros** elemento para cada hierarquia no eixo.  
  
## <a name="customformat"></a>CustomFormat  
 Quando um aplicativo cliente define o **AxisFormat** propriedade *CustomFormat*, o valor será tratado o mesmo que o *TupleFormat* valor por uma instância do Analysis Services.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo a seguir ilustra a estrutura do **eixo** elementos quando um cliente especifica *TupleFormat* ou *CustomFormat* para o **AxisFormat**  Propriedade XMLA, fornecida aos seguintes membros do eixo:  
  
|||||  
|-|-|-|-|  
|Hierarquia de **tempo**|1999|1999|2000|  
|Hierarquia de **categoria**|Real|Orçamento|Orçamento|  
  
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
 O exemplo a seguir ilustra a estrutura do **eixo** elementos quando um cliente especifica *ClusterFormat* para o **AxisFormat** propriedade XMLA, considerando o seguinte membros do eixo:  
  
||||||  
|-|-|-|-|-|  
|Hierarquia de **tempo**|1999|1999|2000|2001|  
|Hierarquia de **categoria**|Real|Orçamento|Orçamento|Orçamento|  
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
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
