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
ms.openlocfilehash: ef3cd31068c324475e8edfe8bf8f7c16acc4a2de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968516"
---
# <a name="tostring-method-datetimeoffset"></a>Método toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna uma representação de cadeia de caracteres do objeto **DateTimeOffset** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma representação de cadeia de caracteres do objeto **DateTimeOffset** .  
  
## <a name="remarks"></a>Remarks  
 A cadeia de caracteres tem o formato *aaaa*-*mm*-*DD * * hh*:*mm*:*SS*[. *fffffff*] [+ |-]*hh*:*mm*.  
  
 Os segundos fracionados da cadeia de caracteres retornada são preenchidas com zeros até obter a precisão declarada. Por exemplo, um **DateTimeOffset (6)** com um valor de "2010-03-10 12:34:56.78-08:00" será formatado por DateTimeOffset. ToString como "2010-03-10 12:34:56.780000-08:00".  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
