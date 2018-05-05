---
title: Elemento ConnectionString (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ConnectionString Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: f74181c4-7df7-4fbd-94dd-e4ad03dffe14
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d08ec61a6e86a133023668496988326f218efbf1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connectionstring-element-assl"></a>Elemento ConnectionString (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a cadeia de caracteres de conexão criptografada para um [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSource>  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Fonte de dados](../../../analysis-services/scripting/objects/datasource-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **ConnectionString** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataSource>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
