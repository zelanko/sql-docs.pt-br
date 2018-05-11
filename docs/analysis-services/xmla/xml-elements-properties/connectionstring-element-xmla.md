---
title: Elemento ConnectionString (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0bf1baf18ffff268f4b82dbb24ced5a8107da23a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="connectionstring-element-xmla"></a>Elemento ConnectionString (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
|Cardinalidade|Veja a tabela abaixo.|  
  
|Ancestral ou pai|Cardinalidade|  
|------------------------|-----------------|  
|[Local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
|[Origem](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [fonte](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para **local** elementos, o **ConnectionString** elemento contém a cadeia de conexão usada pelo **restaurar** ou **sincronizar** comando para atualizar uma fonte de dados local ou se conectar a uma instância remota.  
  
 Para **fonte** elementos, o **ConnectionString** elemento contém a cadeia de conexão usada pelo **sincronizar** comando para se conectar à instância de origem.  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup, restauração e sincronizando bancos de dados & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Restaurar o elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Sincronizar o elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
