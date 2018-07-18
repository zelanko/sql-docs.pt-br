---
title: Elemento AllowOverwrite (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76ba7c6b3046e5298a346cb84472de3ba090e2bc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37972992"
---
# <a name="allowoverwrite-element-xmla"></a>Elemento AllowOverwrite (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Determina se o pai [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) ou [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comando tenta substituir o arquivo de destino ou o banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|Falso|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para os comandos **Backup** , o elemento **AllowOverwrite** determinará se o comando pode substituir o arquivo de backup especificado no elemento **File** .  
  
 Para **restaurar** elementos, o **AllowOverwrite** elemento determina se o comando pode substituir o banco de dados do Analysis Services especificado na **DatabaseName** elemento.  
  
## <a name="see-also"></a>Confira também
 [Elemento DatabaseName &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md)   
 [Elemento de arquivo &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
