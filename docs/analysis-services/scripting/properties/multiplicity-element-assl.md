---
title: Elemento multiplicity (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 441e3829-9009-4b32-a8c6-fa580663387f
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f7d9f031f8976f88e3a9d07e831672d5af2f5fed
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="multiplicity-element-assl"></a>Elemento Multiplicity (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Indica se os atributos em RelationshipEnd estão no lado "um" ou o lado "muitos" de uma relação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEnd>  
   ...  
   <Multiplicity>...</Multiplicity>  
   ...  
</RelationshipEnd>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão||  
|Cardinalidade|1: Elemento requerido que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Um*|Esta é a extremidade de chave primária.|  
|*Muitos*|Esta é a extremidade de chave estrangeira.|  
  
 A enumeração que corresponde aos valores permitidos para **função** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Multiplicity>.  
  
  
