---
title: Elemento Tuple (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Tuple Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32dc7b75f47acf69a8d16e33bc25ac505b1c9333
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061336"
---
# <a name="tuple-element-xmla"></a>Elemento Tuple (XMLA)
  Contém uma coleção de elementos [Member](member-element-xmla.md) contida pelo elemento pai [Tuples](tuples-element-xmla.md).  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Tuplas](tuples-element-xmla.md)|  
|Elementos filho|[Membro](member-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 Quando um aplicativo cliente definir a `AxisFormat` propriedade para *TupleFormat*, um eixo é representado como um conjunto de tuplas. Cada `Axis` elemento contém um `Tuples` elemento que representa o conjunto de tuplas naquele eixo. Cada tupla é representada usando um elemento `Tuple` que contém elementos `Member` de toda hierarquia no eixo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra a estrutura do `Tuple` elemento quando um cliente especifica *TupleFormat* ou *CustomFormat* para o `AxisFormat` propriedade XMLA, considerando o seguinte membros do eixo:  
  
|||||  
|-|-|-|-|  
|Hierarquia de `Time`|1999|1999|2000|  
|Hierarquia de `Category`|Real|Orçamento|Orçamento|  
  
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
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
