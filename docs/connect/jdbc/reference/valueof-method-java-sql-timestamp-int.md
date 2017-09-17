---
title: "Método valueOf (Java.SQL. timestamp, int) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5bd8228a590f165b9df5df8dcc76798dea81e43
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="valueof-method-javasqltimestamp-int"></a>Método valueOf (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um **DateTimeOffset** objeto que representa um ponto no tempo em um deslocamento específico do GMT dados um valor de Java.SQL. timestamp e um valor que indica o deslocamento em minutos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *timestamp*  
  
 Um valorjava.sql.Timestamp.  
  
 *minutesOffset*  
  
 O deslocamento em minutos.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um objeto DateTimeOffset que representa o ponto no tempo fornecido pelo objeto Java.SQL. timestamp no deslocamento especificado, em minutos, do GMT.  
  
## <a name="see-also"></a>Consulte também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
