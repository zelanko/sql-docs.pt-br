---
title: Elemento BackupRemotePartitions (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- BackupRemotePartitions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.backupremotepartitions
- http://schemas.microsoft.com/analysisservices/2003/engine#BackupRemotePartitions
- urn:schemas-microsoft-com:xml-analysis#BackupRemotePartitions
helpviewer_keywords:
- BackupRemotePartitions element
ms.assetid: bd68bcf9-b324-4fa8-b6e5-1f5531f9992c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e18d01ec48264d735a111bc002ca92b08c7b374
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108172"
---
# <a name="backupremotepartitions-element-xmla"></a>Elemento BackupRemotePartitions (XMLA)
  Determina se o pai [Backup](../xml-elements-commands/backup-element-xmla.md) comando faz backup de partições remotas associadas ao objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup>  
   ...  
   <BackupRemotePartitions>...</BackupRemotePartitions>  
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
|Elementos pai|[Backup](../xml-elements-commands/backup-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Se `BackupRemotePartitions` for definido como `True`, um elemento `Locations` que contém um ou mais elementos `Location` deve ser incluído no comando `Backup` ou ocorrerá um erro. Para obter mais informações sobre como fazer backup e restaurar partições remotas, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Locations &#40;XMLA&#41;](locations-element-xmla.md)   
 [Elemento location &#40;XMLA&#41;](location-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
