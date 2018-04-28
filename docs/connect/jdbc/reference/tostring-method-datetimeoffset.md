---
title: Método toString (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: afea2d862b8496d42da20cc9149f764eb4e8c7d5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="tostring-method-datetimeoffset"></a>Método toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna uma representação de cadeia de caracteres da **DateTimeOffset** objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Uma representação de cadeia de caracteres da **DateTimeOffset** objeto.  
  
## <a name="remarks"></a>Remarks  
 A cadeia de caracteres tem o formato *aaaa*-*MM*-*DD * * hh*:*mm*:*ss*[. *FFFFFFF*] [+ |-]*hh*:*mm*.  
  
 Os segundos fracionados da cadeia de caracteres retornada são preenchidas com zeros até obter a precisão declarada. Por exemplo, um **datetimeoffset(6)** com um valor de "2010-03-10 12:34:56.78 -08:00" será formatado por DateTimeOffset como "2010-03-10 12:34:56.780000 -08:00".  
  
## <a name="see-also"></a>Consulte também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
