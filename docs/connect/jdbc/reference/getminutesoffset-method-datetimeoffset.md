---
title: Método getMinutesOffset (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fc9351769b77c9f6d873c0875d8629c0ccfc805
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getminutesoffset-method-datetimeoffset"></a>Método getMinutesOffset (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o deslocamento em minutos GMT, do objeto DateTimeOffset.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 O deslocamento em minutos.  
  
## <a name="remarks"></a>Remarks  
 Para um objeto DateTimeOffset que representa 8 de março de 2010, 11:35:48 -0800, getMinutesOffset retorna o valor 480.  
  
## <a name="see-also"></a>Consulte também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
