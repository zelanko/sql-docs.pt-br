---
title: Elemento New (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ed98ed9c42d8cecddb07941855403925b1de6b8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575918"
---
# <a name="new-element-xmla"></a>Elemento New (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Pasta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O **novo** elemento contém um caminho UNC que substitui o valor da **Original** elemento contido pelo pai **pasta** elemento para todos os objetos restaurados ou sincronizados, respectivamente, durante um **restaurar** ou **sincronizar** comando. O valor da **Original** elemento é comparado com o valor da **StorageLocation** elemento para cada cubo, grupo de medidas ou partição e, se uma correspondência for encontrada, o valor desse elemento é usado para atualizar o **StorageLocation** do objeto durante a restauração ou sincronização.  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup e restaurando objetos (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Confira também
 [Elemento original &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)   
 [Elemento Restore &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Elemento StorageLocation &#40;ASSL&#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [Elemento Synchronize &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
