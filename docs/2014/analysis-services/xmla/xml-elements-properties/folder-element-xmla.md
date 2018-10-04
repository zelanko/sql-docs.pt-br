---
title: Elemento folder (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Folder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords:
- Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70c5258edefa19d2858c40648aa742f75a9a1e49
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055117"
---
# <a name="folder-element-xmla"></a>Elemento Folder (XMLA)
  Contém um local de armazenamento do sistema de arquivos a ser atualizado para um [local](location-element-xmla.md) elemento durante uma [restaurar](../xml-elements-commands/restore-element-xmla.md) ou [sincronizar](../xml-elements-commands/synchronize-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Folders>  
   ...  
   <Folder>  
      <Original>...</Original>  
      <New>...</New>  
   </Folder>  
   ...  
</Folders>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Pastas](folders-element-xmla.md)|  
|Elementos filho|[Novos](new-element-xmla.md), [Original](original-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Folder`, se for especificado, altera os locais de armazenamento dos objetos contidos pelo arquivo de backup (para os comandos `Restore`) ou pelo banco de dados na instância de origem (para os comandos `Synchronize`) que correspondem ao valor do elemento `Original` para o valor do elemento `New`.  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento StorageLocation &#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
