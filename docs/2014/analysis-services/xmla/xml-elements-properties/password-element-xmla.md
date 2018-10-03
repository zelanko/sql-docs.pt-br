---
title: Elemento Password (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Password
- urn:schemas-microsoft-com:xml-analysis#Password
- microsoft.xml.analysis.password
helpviewer_keywords:
- Password element
ms.assetid: 8a0603bd-f6a1-4b86-84f1-c83d0b03951b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a72d111dd6bccec8b6b40440a0e40e5a6669d87e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159176"
---
# <a name="password-element-xmla"></a>Elemento Password (XMLA)
  Determina a senha a ser usada pelo pai [Backup](../xml-elements-commands/backup-element-xmla.md) ou [restaurar](../xml-elements-commands/restore-element-xmla.md) comando para criptografar ou descriptografar um arquivo de backup.  
  
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
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Backup](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para comandos `Backup`, se o elemento `Password` não estiver incluído ou contiver uma cadeia de caracteres vazia, o arquivo de backup não será criptografado.  
  
 Para comandos `Restore`, se o elemento `Password` não estiver incluído ou contiver uma cadeia de caracteres vazia ao tentar restaurar um arquivo de backup criptografado, ocorrerá um erro.  
  
 Se os elementos `Location` estiverem incluídos em um comando `Backup` ou `Restore`, o mesmo elemento `Password` será usado para os arquivos de backup e de backup remoto. Para obter mais informações sobre arquivos de backup remotos, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento location &#40;XMLA&#41;](location-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
