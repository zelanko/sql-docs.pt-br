---
title: Elemento Insert (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: Insert Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Insert
- http://schemas.microsoft.com/analysisservices/2003/engine#Insert
- microsoft.xml.analysis.insert
helpviewer_keywords: Insert command
ms.assetid: d1137033-cc19-4bcb-b93d-8575f17bea6b
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 21a7e8cc50293eebbbeeaf1f2850b32a71dcf792
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="insert-element-xmla"></a>Elemento Insert (XMLA)
  Insere membros de atributo em uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Insert>  
      <Object>...</Object>  
      <Attributes>...</Attributes>  
   </Insert>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md), [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O comando **Insert** insere novos membros de atributo em uma dimensão habilitada para gravação.  
  
 Para obter mais informações sobre a exclusão de membros, consulte [inserir, atualizar e remover membros &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Remover elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Atualizar o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
