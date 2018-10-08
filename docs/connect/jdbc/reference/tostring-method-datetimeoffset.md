---
title: Método toString (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 990cb7cccd972ac926824ca3f8d99de3f0d6e305
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687734"
---
# <a name="tostring-method-datetimeoffset"></a>Método toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna uma representação de cadeia de caracteres da **DateTimeOffset** objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma representação de cadeia de caracteres da **DateTimeOffset** objeto.  
  
## <a name="remarks"></a>Remarks  
 A cadeia de caracteres tem o formato *aaaa*-*MM*-*DD * * hh*:*mm*:*ss*[. *FFFFFFF*] [+ |-]*hh*:*mm*.  
  
 Os segundos fracionados da cadeia de caracteres retornada são preenchidas com zeros até obter a precisão declarada. Por exemplo, uma **datetimeoffset(6)** com um valor de "12:34:56.78 2010-03-10-08:00" será formatado por ToString como "12:34:56.780000 2010-03-10-08:00".  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
