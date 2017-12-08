---
title: Elemento DataSource (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DataSource Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DataSource
helpviewer_keywords: DataSource element
ms.assetid: 113fba1c-2679-4d06-9339-90a4a76f9b31
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a561f0ef13479baf8a6f8bebbe73ae23c74201ae
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="datasource-element-assl"></a>Elemento DataSource (ASSL)
  Define uma fonte de dados em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSources>  
   <DataSource xsi:type="RelationalDataSource">...</DataSource>  
   <!-- or -->  
   <DataSource xsi:type="OlapDataSource">...</DataSource>  
   <!-- or -->  
   <DataSource xsi:type="PushedDataSource">...</DataSource>  
</DataSources>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[RelationalDataSource](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md), [OlapDataSource](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md), [PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Fontes de dados](../../../analysis-services/scripting/collections/datasources-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DataSource>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de banco de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
