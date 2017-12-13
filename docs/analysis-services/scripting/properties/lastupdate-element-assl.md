---
title: Elemento LastUpdate (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: LastUpdate Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: LastUpdate element
ms.assetid: 639db733-a082-4f57-868d-a3bcd5e7a4f6
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e1f1e67f477c150fcb438bec025efcc3045f15d5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="lastupdate-element-assl"></a>Elemento LastUpdate (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém somente leitura carimbo de hora que indica a última vez em que o associado [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) ou qualquer um dos principais objetos que contém o banco de dados foi alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database> <!-- or one of the elements that are listed in the Element Relationships table -->  
   ...  
   <LastUpdate>...</LastUpdate>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|DateTime|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de **LastUpdate** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
