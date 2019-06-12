---
title: Método setString (long, java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fb59b09-e825-46a6-ba5d-85d4a8dc143a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 604e39fcf2d8bd6bfb218fe33fda391c2b53403a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66762236"
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
 *pos*  
  
 A posição em que a gravação deve ser iniciada no CLOB.  
  
 *str*  
  
 A cadeia de caracteres a ser gravada no CLOB.  
  
 *offset*  
  
 O deslocamento dentro da cadeia de caracteres de onde se inicia a leitura dos caracteres.  
  
 *len*  
  
 O número de caracteres a serem gravados.  
  
## <a name="return-value"></a>Valor retornado  
 O número de caracteres gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método setString é especificado pelo método setString na interface java.sql.CallableStatement.  
  
 Os dados de caractere são substituídos iniciando na posição especificada e podem substituir o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará a cadeia de caracteres. A especificação de um valor posição +2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setString &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
