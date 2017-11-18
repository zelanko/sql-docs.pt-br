---
title: "setString (long, Java, int, int) do método | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerClob.setString (long, java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fb59b09-e825-46a6-ba5d-85d4a8dc143a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 362cd4df54ee5ad826d2313341cd9ba4c7253546
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-long-javalangstring-int-int"></a>Método setString (long, java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava a cadeia de caracteres fornecida no CLOB, começando na posição fornecida e com base no deslocamento e comprimento fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int setString(long pos,  
                     java.lang.String str,  
                     int offset,  
                     int len)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição em que a gravação deve ser iniciada no CLOB.  
  
 *STR*  
  
 A cadeia de caracteres a ser gravada no CLOB.  
  
 *deslocamento*  
  
 O deslocamento dentro da cadeia de caracteres de onde se inicia a leitura dos caracteres.  
  
 *Len*  
  
 O número de caracteres a serem gravados.  
  
## <a name="return-value"></a>Valor de retorno  
 O número de caracteres gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método setString é especificado pelo método setString na interface do CLOB.  
  
 Os dados de caractere são substituídos iniciando na posição especificada e podem substituir o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará a cadeia de caracteres. A especificação de um valor posição +2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte também  
 [Método setString &#40; SQLServerClob &#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

