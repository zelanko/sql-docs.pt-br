---
title: Elemento TableID (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: TableID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TableID
helpviewer_keywords: TableID element
ms.assetid: 45fe7e23-b274-4bc2-be63-1a5bb6680f51
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e5fff4e89787afd9f845e68dee89bb10c6bb0274
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="tableid-element-assl"></a>Elemento TableID (ASSL)
  Contém o identificador (ID) da tabela (da [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) elemento) associada ao elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ColumnBinding> <!-- or DSVTableBinding, RowBinding, IncrementalProcessingNotification -->  
   ...  
   <TableID>...</TableID>  
   ...  
</ColumnBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [DSVTableBinding](../../../analysis-services/scripting/data-type/dsvtablebinding-data-type-assl.md), [IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md), [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 A tabela identificada por **TableID** deve estar dentro da fonte de dados ao qual o objeto proprietário (dimensão ou cubo) está associado.  
  
 Os elementos que correspondem aos pais de **TableID** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.ColumnBinding>, <xref:Microsoft.AnalysisServices.DSVTableBinding>, <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>, e <xref:Microsoft.AnalysisServices.RowBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
