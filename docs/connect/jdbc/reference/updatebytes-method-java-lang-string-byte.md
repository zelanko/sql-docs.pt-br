---
title: Método updateBytes (Java, byte) | Microsoft Docs
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
- SQLServerResultSet.updateBytes (java.lang.String, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fb9de2b-61bc-4c96-89a5-c07cd7ee201a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8403b8014ecfe106b2949a64743a67481b85a86e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updatebytes-method-javalangstring-byte"></a>Método updateBytes (Java, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com uma matriz de **bytes** considerando o nome da coluna de valores.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBytes(java.lang.String columnName,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
 *x*  
  
 Uma matriz de **bytes** valores.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateBytes é especificado pelo método updateBytes na interface Java.SQL. resultset.  
  
 Em uma versão anterior do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], você pode usar Updatebytes para converter valores entre matrizes de bytes e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de dados **data**, **tempo**,  **datetime2**, ou **datetimeoffset**. Agora, ao usar esse método com esses tipos de dados, ocorrerá uma exceção indicando que não há suporte para a conversão.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateBytes &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
