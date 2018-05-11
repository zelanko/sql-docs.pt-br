---
title: Elemento original (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 53c758b59121d798cad86d4e9de5f52db36cb278
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="original-element-xmla"></a>Elemento Original (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém o local de armazenamento de sistema arquivos original usado por um [pasta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
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
  
## <a name="remarks"></a>Remarks  
 O **Original** elemento contém um caminho UNC para ser substituído pelo valor da [novo](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md) elemento contido pelo pai **pasta** elemento para todos os objetos restaurados ou sincronizados, respectivamente, durante um [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) ou [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando. O valor desse elemento é comparado ao valor da [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md) elemento para cada cubo, grupo de medidas ou partição e, se uma correspondência for encontrada, o valor da **novo** elemento é usado para atualizar o  **StorageLocation** do objeto durante a restauração ou sincronização.  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup, restauração e sincronizando bancos de dados & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
