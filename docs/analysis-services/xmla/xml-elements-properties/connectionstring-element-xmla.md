---
title: Elemento ConnectionString (XMLA) | Microsoft Docs
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
- ConnectionString Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.connectionstring
- urn:schemas-microsoft-com:xml-analysis#ConnectionString
- http://schemas.microsoft.com/analysisservices/2003/engine#ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: 3b0575aa-79ed-4f14-ae7e-dd587af4cdb1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6c6227db17c74b4c33d07abfcd809ae01bc3a9a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="connectionstring-element-xmla"></a>Elemento ConnectionString (XMLA)
  Contém uma cadeia de caracteres de conexão usada pelo pai [local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) ou [fonte](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|Consulte a tabela a seguir.|  
  
|Ancestral ou pai|Cardinalidade|  
|------------------------|-----------------|  
|[Local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
|[Origem](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [fonte](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Para **local** elementos, o **ConnectionString** elemento contém a cadeia de conexão usada pelo **restaurar** ou **sincronizar** comando para atualizar uma fonte de dados local ou se conectar a uma instância remota.  
  
 Para **fonte** elementos, o **ConnectionString** elemento contém a cadeia de conexão usada pelo **sincronizar** comando para se conectar à instância de origem.  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup, restauração e sincronizando bancos de dados &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Restaurar o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Sincronizar o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

