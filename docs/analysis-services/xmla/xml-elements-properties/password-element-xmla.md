---
title: Elemento Password (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f82fbcfecff5e6d216c3758ce442d82591a24d78
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050417"
---
# <a name="password-element-xmla"></a>Elemento Password (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Determina a senha a ser usada pelo pai [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) ou [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comando para criptografar ou descriptografar um arquivo de backup.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Password>...</Password>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para comandos **Backup** , se o elemento **Password** não estiver incluído ou contiver uma cadeia de caracteres vazia, o arquivo de backup não será criptografado.  
  
 Para comandos **Restore** , se o elemento **Password** não estiver incluído ou contiver uma cadeia de caracteres vazia ao tentar restaurar um arquivo de backup criptografado, ocorrerá um erro.  
  
 Se os elementos **Location** estiverem incluídos em um comando **Backup** ou **Restore** , o mesmo elemento **Password** será usado para os arquivos de backup e de backup remoto. Para obter mais informações sobre arquivos de backup remotos, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Confira também
 [Elemento location &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
