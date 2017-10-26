---
title: "Método valueOf (Java.SQL. timestamp, java.util.Calendar) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b77f9ce80c54980a8a55d23b90667e2c07672caa
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>Método valueOf (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um **DateTimeOffset** objeto que representa um ponto no tempo em um deslocamento específico do GMT dados um valor de Java.SQL. timestamp e um valor de java.util.Calendar indicando o deslocamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *timestamp*  
  
 Um valorjava.sql.Timestamp.  
  
 *calendário*  
  
 O valor de deslocamento.  Os componentes de data e hora de *calendário* será definida de acordo com o *timestamp* valor.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um objeto DateTimeOffset que representa o ponto no tempo fornecido pelo objeto Java.SQL. timestamp no fuso horário do objeto java.util.Calendar determinado.  
  
## <a name="remarks"></a>Comentários  
 Esse método também define o objeto de java.util.Calendar para o ponto no tempo fornecido pelo objeto Java.SQL. timestamp.  
  
## <a name="see-also"></a>Consulte também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

