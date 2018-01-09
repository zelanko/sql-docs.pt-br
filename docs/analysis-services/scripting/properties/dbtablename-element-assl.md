---
title: Elemento DbTableName (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DbTableName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DbTableName
helpviewer_keywords: DbTableName element
ms.assetid: 842cae85-ab9c-4c75-ab44-51a4d9b1b943
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e7ab467cf2b2d9445789389ff41b9df726c1c8c4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="dbtablename-element-assl"></a>Elemento DbTableName (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o nome da tabela à qual está associado ao elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TableBinding> <!-- or TableNotification -->  
   ...  
   <DbTableName>...</DbTableName>  
   ...  
</TableBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md), [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Os elementos que correspondem aos pais de **DbTableName** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.TableBinding> e <xref:Microsoft.AnalysisServices.TableNotification>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
