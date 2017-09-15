---
title: "Método getString (int) (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa493c4-fe07-449b-b4d0-384e1a1fce48
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2851090b2f22faac3f050ad535ec9f36ac3efae6
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getstring-method-int-sqlserverresultset"></a>Método getString (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do índice de coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **cadeia de caracteres** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getString(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getString é especificado pelo método getString na interface Java.SQL. resultset.  
  
 Todas as colunas na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] pode ser retornado como uma cadeia de caracteres. Isso significa que um **cadeia de caracteres** representação de todos os tipos baseados em número e baseados em caracteres e uma representação de cadeia de caracteres hexadecimais de colunas binárias, como binary, varbinary, varbinary (max), imagem, timestamp e uniqueidentifier, podem ser retornado.  
  
 Os tipos que diferenciam locais, como money, smallmoney, datetime, smalldatetime, float, real, decimal e numeric, retornarão o formato toString() canônico para o valor subjacente do tipo.  
  
 Tipos definidos pelo usuário são retornados como hexadecimal **cadeia de caracteres** valores.  
  
## <a name="see-also"></a>Consulte também  
 [Método getString &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
