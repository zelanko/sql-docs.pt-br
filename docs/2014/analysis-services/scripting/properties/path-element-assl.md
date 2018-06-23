---
title: Elemento path (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Path Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Path
helpviewer_keywords:
- Path element
ms.assetid: 0edc59ac-1671-4fe1-9b7c-6c1548df5c63
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5ba53c4ee4399a39ebd8e4a1b14c9c062b3abaa7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010107"
---
# <a name="path-element-assl"></a>Elemento Path (ASSL)
  Contém o caminho, conforme fornecido por uma instância de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], de um relatório usado pelo [ReportAction](../data-type/action-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ReportAction>  
   ...  
   <Path>...</Path>  
   ...  
</ReportAction>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: Elemento opcional que ocorre apenas uma vez|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ReportAction](../data-type/action-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do `Path` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  