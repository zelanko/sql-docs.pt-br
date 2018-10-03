---
title: Método getMinutesOffset (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5f135ac405a5dbeda6a0c86d447e591c8bee9a1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755334"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>Método getMinutesOffset (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o deslocamento, em minutos GMT desse objeto DateTimeOffset.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Valor retornado  
 O deslocamento em minutos.  
  
## <a name="remarks"></a>Remarks  
 Para um objeto DateTimeOffset que representa 8 de março de 2010, 11:35:48 getMinutesOffset de-0800, retorna o valor 480.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
