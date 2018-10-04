---
title: Elemento ID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ID
helpviewer_keywords:
- ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71de55c773ce75ec75b38b774ad0a5e8ec35ed9b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48170256"
---
# <a name="id-element-assl"></a>Elemento ID (ASSL)
  Contém o ID (Identificador exclusivo) do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
   <ID>...</ID>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (até 100 caracteres)|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Ação](../objects/action-element-assl.md), [agregação](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [cubo](../objects/cube-element-assl.md), [CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [banco de dados](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [dimensão ](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [hierarquia](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [nível](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Medida](../objects/measure-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MeasureGroupBinding](../data-type/binding-data-type-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [ MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [partição](../objects/partition-element-assl.md), [permissão](../data-type/permission-data-type-assl.md), [Perspectiva](../objects/perspective-element-assl.md), [função](../objects/role-element-assl.md), [servidor](../objects/server-element-assl.md), [rastreamento](../objects/trace-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Todo objeto principal em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tem um `ID` elemento como uma propriedade. O valor de um `ID` elemento tem as seguintes restrições:  
  
-   O valor não pode conter espaços à esquerda ou direita. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] removerá, de forma implícita, os espaços à esquerda ou direita do valor de um elemento `ID`.  
  
-   O valor não pode conter caracteres de controle. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] removerá os caracteres de controle implicitamente do valor de um elemento `ID`.  
  
-   Os valores reservados a seguir não podem ser usados:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 a COM9 (COM1, COM2, COM3 e assim por diante)  
  
    -   CON  
  
    -   LPT1 a LPT9 (LPT1, LPT2, LPT3 e assim por diante)  
  
    -   NUL  
  
    -   PRN  
  
 A tabela a seguir lista os caracteres adicionais que não podem ser usados dentro do valor de um `ID` elemento, dependendo do elemento pai.  
  
|Elemento pai|Caracteres|  
|--------------------|----------------|  
|[Servidor](../objects/server-element-assl.md)|O valor deve seguir as regras para nomes do computador Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. (Endereços IP não são válidos)|  
|[Fonte de dados](../objects/datasource-element-assl.md)|:/\\*&#124;?" [()]{}<>|  
|[Nível](../objects/level-element-assl.md), [elemento atributo](../objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! [] de + ={}<>|  
|Todos os outros elementos pai|.,;' `:/\\*&#124;?" & % $! [] () de + ={}<>|  
  
## <a name="see-also"></a>Consulte também  
 [Nomeie o elemento &#40;ASSL&#41;](name-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
