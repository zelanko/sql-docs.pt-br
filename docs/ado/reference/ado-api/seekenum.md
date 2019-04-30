---
title: SeekEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e044c4a2cda01fcc9cbba2667beaae75a12caf
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63459338"
---
# <a name="seekenum"></a>SeekEnum
Especifica o tipo de [busca](../../../ado/reference/ado-api/seek-method.md) para executar.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Procura a primeira chave igual a *KeyValues*.|  
|**adSeekLastEQ**|2|A última chave igual de buscas *KeyValues*.|  
|**adSeekAfterEQ**|4|Buscas de uma chave igual a *KeyValues* ou depois de onde essa correspondência teria ocorrido.|  
|**adSeekAfter**|8|Procura uma chave depois de onde uma correspondência com *KeyValues* teria ocorrido.|  
|**adSeekBeforeEQ**|16|Buscas de uma chave igual a *KeyValues*ou antes de onde essa correspondência teria ocorrido.|  
|**adSeekBefore**|32|Buscas imediatamente antes de uma chave em que uma correspondência com *KeyValues* teria ocorrido.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
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
