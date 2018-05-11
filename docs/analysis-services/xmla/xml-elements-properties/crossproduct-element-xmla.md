---
title: Elemento CrossProduct (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f67968b92fe879a6675222ed57306fca9a317b31
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="crossproduct-element-xmla"></a>Elemento CrossProduct (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém um produto cruzado entre conjuntos ordenados de membros de cada hierarquia para um [eixo](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) elemento que usa o [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) retornado pelo tipo de dados, o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Eixo](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|Elementos filho|[Membros](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Description|  
|---------------|-----------------|  
|Tamanho|Necessário **inteiro** atributo. Indica o número de tuplas contido no produto cruzado representado pelo **CrossProduct** elemento.|  
  
## <a name="remarks"></a>Remarks  
 Quando um aplicativo cliente define o **AxisFormat** propriedade *ClusterFormat*, os membros em cada eixo são divididos em clusters nos quais cada cluster representa um produto cruzado entre conjuntos ordenados de membros de cada hierarquia. Cada cluster é representado por um **CrossProduct** elemento. Cada **CrossProduct** elemento contém um **membros** elemento para cada hierarquia no eixo. Um **CrossProduct** elemento pode conter membros de uma única hierarquia.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra a estrutura do **CrossProduct** elemento quando um cliente especifica *ClusterFormat* para o **AxisFormat** propriedade XMLA, considerando o membros a seguir para o eixo:  
  
||||||  
|-|-|-|-|-|  
|Hierarquia de **tempo**|1999|1999|2000|2001|  
|Hierarquia de **categoria**|Real|Orçamento|Orçamento|Orçamento|  
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
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
