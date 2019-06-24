---
title: Método setString (long, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b23c0c5de87fc5df557d5d02958a72eaa336f8fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771670"
---
# <a name="setstring-method-long-javalangstring"></a>Método setString (long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava o **String** fornecido no CLOB, começando na posição fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 A posição em que a gravação deve ser iniciada no CLOB.  
  
 *s*  
  
 A **cadeia de caracteres** a ser gravada no CLOB.  
  
## <a name="return-value"></a>Valor retornado  
 O número de caracteres gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método setString é especificado pelo método setString na interface java.sql.Clob.  
  
 Os dados de caractere são substituídos iniciando na posição especificada e podem ultrapassar o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará a cadeia de caracteres. A especificação de valores de posição+2 ou maiores (ou zero ou menos) causarão o lançamento de um erro de posição.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setString &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
