---
title: Elemento DataSources (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 479b88873d95f9728fdf916502ff527377d5831d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="datasources-element-assl"></a>Elemento DataSources (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a coleção de [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) elementos associados a um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database>  
   ...  
   <DataSources>  
      <DataSource>...</DataSource>  
   </DataSources>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Elementos filho|[Fonte de dados](../../../analysis-services/scripting/objects/datasource-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DataSourceCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
