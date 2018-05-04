---
title: Método (Java) (SQLServerResultSet) getByte | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerResultSet.getByte (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 069c68ff-442d-4104-917f-3445a3ad264a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24f47eabe5f89dc7cdbb419dffe44cb4af21bd36
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getbyte-method-javalangstring-sqlserverresultset"></a>getByte método (Java) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **bytes** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public byte getByte(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **bytes** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getByte é especificado pelo método getByte na interface Java.SQL. resultset.  
  
 Esse método tem suporte apenas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de dados que podem retornar com segurança um valor de byte, como tinyint e bit. Todos os outros tipos de dados fazem com que uma exceção seja lançada.  
  
## <a name="see-also"></a>Consulte também  
 [Método getByte &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
