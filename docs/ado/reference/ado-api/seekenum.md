---
title: SeekEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 40c15bd116b4e0a7ba13127dc48ec18421b5924b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="seekenum"></a>SeekEnum
Especifica o tipo de [busca](../../../ado/reference/ado-api/seek-method.md) para executar.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Procura a primeira chave igual a *KeyValues*.|  
|**adSeekLastEQ**|2|Busca a última chave igual a *KeyValues*.|  
|**adSeekAfterEQ**|4|Procura uma chave igual a *KeyValues* ou depois que teria ocorrido correspondentes.|  
|**adSeekAfter**|8|Procura uma chave depois de onde uma correspondência com *KeyValues* teria ocorrido.|  
|**adSeekBeforeEQ**|16|Procura uma chave igual a *KeyValues*ou antes que teria ocorrido correspondentes.|  
|**adSeekBefore**|32|Buscas imediatamente antes de uma chave quando uma correspondência com *KeyValues* teria ocorrido.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC Equivalent  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Seek](../../../ado/reference/ado-api/seek-method.md)
