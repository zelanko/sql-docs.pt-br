---
title: "Método (Java) getCharacterStream | Microsoft Docs"
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
- SQLServerResultSet.getCharacterStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cdddc572-05c1-480d-b3e5-28270001575c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a882e903e689f67db7adf9b8d71d34851affd5b4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-javalangstring"></a>Método getCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto Java.IO. Reader.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Reader getCharacterStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto do leitor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getCharacterStream é especificado pelo método getCharacterStream na interface Java.SQL. resultset.  
  
 Esse método lerá apenas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de dados de caractere Unicode, como nchar, nvarchar, nvarchar (max) e ntext. Todos os outros tipos de dados, incluindo os tipos de caracteres ASCII, fazem com que uma exceção seja lançada. Para ler os tipos de dados ASCII, use o [getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [Método getCharacterStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

