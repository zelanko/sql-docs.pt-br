---
title: Elemento New (XMLA) | Microsoft Docs
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
apiname: New Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#New
- microsoft.xml.analysis.new
- urn:schemas-microsoft-com:xml-analysis#New
helpviewer_keywords: New element
ms.assetid: 1321adcb-67f7-40f0-8f20-b17c1d3e3f17
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: afe70a458877ea83328075873c2cd510a4bdf41a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="new-element-xmla"></a>Elemento New (XMLA)
  Contém o novo local de armazenamento de sistema de arquivos usado por um [pasta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
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
|Elementos pai|[Pasta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **novo** elemento contém um caminho UNC que substitui o valor da **Original** elemento contido pelo pai **pasta** elemento para todos os objetos restaurados ou sincronizados, respectivamente, durante um **restaurar** ou **sincronizar** comando. O valor da **Original** elemento é comparado com o valor da **StorageLocation** elemento para cada cubo, grupo de medidas ou partição e, se uma correspondência for encontrada, o valor desse elemento é usado para atualizar o **StorageLocation** do objeto durante a restauração ou sincronização.  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup e restaurando objetos (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Original elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)   
 [Restaurar o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Elemento StorageLocation &#40; ASSL &#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [Sincronizar o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
