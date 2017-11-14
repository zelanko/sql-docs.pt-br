---
title: SeekEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 051f4e1c300796e2777e9b06a1514c9ce00b9b02
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="seekenum"></a>SeekEnum
Especifica o tipo de [busca](../../../ado/reference/ado-api/seek-method.md) para executar.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Procura a primeira chave igual a *KeyValues*.|  
|**adSeekLastEQ**|2|Busca a última chave igual a *KeyValues*.|  
|**adSeekAfterEQ**|4|Procura uma chave igual a *KeyValues* ou depois que teria ocorrido correspondentes.|  
|**adSeekAfter**|8|Procura uma chave depois de onde uma correspondência com *KeyValues* teria ocorrido.|  
|**adSeekBeforeEQ**|16|Procura uma chave igual a *KeyValues*ou antes que teria ocorrido correspondentes.|  
|**adSeekBefore**|32|Buscas imediatamente antes de uma chave quando uma correspondência com *KeyValues* teria ocorrido.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
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

