---
title: Elemento AllowOverwrite (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllowOverwrite Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.allowoverwrite
- urn:schemas-microsoft-com:xml-analysis#EndSession
helpviewer_keywords:
- AllowOverwrite element
ms.assetid: e7e92481-5f29-47f2-9efd-4e5e60c002bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb0d58570349fbbb17b442ddebc0fd3193531149
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131426"
---
# <a name="allowoverwrite-element-xmla"></a>Elemento AllowOverwrite (XMLA)
  Determina se o pai [Backup](../xml-elements-commands/backup-element-xmla.md) ou [restaurar](../xml-elements-commands/restore-element-xmla.md) comando tenta substituir o arquivo de destino ou o banco de dados.  
  
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
|Elementos pai|[Backup](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para os comandos `Backup`, o elemento `AllowOverwrite` determinará se o comando pode substituir o arquivo de backup especificado no elemento `File`.  
  
 Para `Restore` elementos, o `AllowOverwrite` elemento determina se o comando pode substituir o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no `DatabaseName` elemento.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento DatabaseName &#40;XMLA&#41;](name-element-xmla.md)   
 [Elemento de arquivo &#40;XMLA&#41;](file-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
