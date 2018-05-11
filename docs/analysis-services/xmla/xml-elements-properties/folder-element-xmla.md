---
title: Elemento folder (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a13ac1689c58519a6e8d1ac06cacc8357570b75
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="folder-element-xmla"></a>Elemento Folder (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém um local de armazenamento do sistema de arquivos a ser atualizado para um [local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) elemento durante uma [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) ou [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Pastas](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|Elementos filho|[Novo](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md), [Original](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento **Folder** , se for especificado, altera os locais de armazenamento dos objetos contidos pelo arquivo de backup (para os comandos **Restore** ) ou pelo banco de dados na instância de origem (para os comandos **Synchronize** ) que correspondem ao valor do elemento **Original** para o valor do elemento **New** .  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup, restauração e sincronizando bancos de dados & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento StorageLocation & #40; ASSL & #41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
