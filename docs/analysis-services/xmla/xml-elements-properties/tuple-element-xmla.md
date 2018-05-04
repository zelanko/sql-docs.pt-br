---
title: Elemento Tuple (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Tuple Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 194bcb41a54fe4255055e9b64a69f084e9d5a1cf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="tuple-element-xmla"></a>Elemento Tuple (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma coleção de elementos [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) contida pelo elemento pai [Tuples](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Tuples>  
   <Tuple>  
      <Member>...</Member>  
   </Tuple>  
   ...  
</Tuples>  
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
|Elementos pai|[Tuplas](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
|Elementos filho|[Membro](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Quando um aplicativo cliente definir a propriedade **AxisFormat** como *TupleFormat*, um eixo é representado como um conjunto de tuplas. Cada elemento **Axis** contém um elemento **Tuples** que representa o conjunto de tuplas naquele eixo. Cada tupla é representada usando um elemento **Tuple** que contém elementos **Member** de toda hierarquia no eixo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra a estrutura do elemento **Tuple** quando um cliente especifica *TupleFormat* ou *CustomFormat* para a propriedade XMLA do **AxisFormat**, fornecida aos seguintes membros do eixo:  
  
|||||  
|-|-|-|-|  
|Hierarquia de **tempo**|1999|1999|2000|  
|Hierarquia de **categoria**|Real|Orçamento|Orçamento|  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
