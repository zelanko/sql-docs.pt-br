---
title: Elemento (XMLA) do banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Database Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.database
- http://schemas.microsoft.com/analysisservices/2003/engine#Database
- urn:schemas-microsoft-com:xml-analysis#Database
helpviewer_keywords:
- Database element
ms.assetid: 2ded06c4-4eaf-4ccb-a416-41ee51ced8bc
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b21cc8a503c2da54c7d5f30e643da6a4e9a090dd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="database-element-xmla"></a>Elemento Database (XMLA)
  Identifica o banco de dados que contém a dimensão representada pelo pai [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Object>  
   ...  
   <Database>...</Database>  
   ...  
</Object>  
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
|Elementos pai|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **banco de dados** elemento é um identificador de objeto que contém o nome do banco de dados do Analysis Services que contém a dimensão representada pelo **objeto** elemento.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Cube &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md)   
 [Elemento Dimension &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

