---
title: Elemento LastUpdate (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LastUpdate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- LastUpdate element
ms.assetid: 639db733-a082-4f57-868d-a3bcd5e7a4f6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 940c8dfb2bbd74d431024b70673a38bbc5fc7ee6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069318"
---
# <a name="lastupdate-element-assl"></a>Elemento LastUpdate (ASSL)
  Contém somente leitura carimbo de hora que indica a última vez em que o associado [banco de dados](../objects/database-element-assl.md) ou qualquer objeto principal que contém o banco de dados foi alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database> <!-- or one of the elements that are listed in the Element Relationships table -->  
   ...  
   <LastUpdate>...</LastUpdate>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|DateTime|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Banco de dados](../objects/database-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de `LastUpdate` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
