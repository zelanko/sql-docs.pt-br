---
title: Elemento DataSource (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
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
ms.openlocfilehash: bfc12e594ff560c3f181ec194153412da8451877
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="datasource-element-assl"></a>Elemento DataSource (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define uma fonte de dados em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[RelationalDataSource](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md), [OlapDataSource](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md), [PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Fontes de dados](../../../analysis-services/scripting/collections/datasources-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DataSource>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento de banco de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
