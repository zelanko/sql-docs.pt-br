---
title: Elemento AggregationPrefix (ASSL) | Microsoft Docs
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
- AggregationPrefix Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 84f7b086e1cdc2516f0912a4580d0b3eb45132ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122494"
---
# <a name="aggregationprefix-element-assl"></a>Elemento AggregationPrefix (ASSL)
  Define o prefixo comum a ser usado para nomes de agregação no elemento pai associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../objects/cube-element-assl.md), [banco de dados](../objects/database-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [partição](../objects/partition-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Prefixos de agregação geram os nomes de agregação em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e também gerar nomes de tabela no banco de dados relacional para agregações armazenadas em uma partição OLAP (ROLAP) relacional.  
  
 Um nome de agregação completamente expandido tem as partes a seguir:  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 As primeiras quatro partes do nome de agregação compõem o prefixo de agregação. O usuário fornece as primeiras quatro partes:  
  
-   *DatabasePrefix* representa o valor da `AggregationPrefix` elemento associado a um `Database` elemento.  
  
-   *CubePrefix* representa o valor da `AggregationPrefix` elemento associado a um `Cube` elemento.  
  
-   *MeasureGroupPrefix* representa o valor da `AggregationPrefix` elemento associado a um `MeasureGroup` elemento.  
  
-   *PartitionPrefix* representa o valor da `AggregationPrefix` elemento associado a um `Partition` elemento.  
  
 A quinta parte do nome, *AggregationID*, é uma ID definida pelo sistema, e os usuários não têm nenhum controle sobre essa parte do nome.  
  
 Os elementos que correspondem aos pais de `AggregationPrefix` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  