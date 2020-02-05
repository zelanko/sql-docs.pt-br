---
title: Método getString (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a98c8a8-61d0-40c9-9335-25a87b732dc3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8961f6b67a4b22370d6712e44616036631d1935
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979482"
---
# <a name="getstring-method-javalangstring-sqlserverresultset"></a>Método getString (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como uma **String** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getString(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor de **String**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getString é especificado pelo método getString na interface java.sql.ResultSet.  
  
 Todas as colunas no SQL Server podem ser retornadas como uma String. Isso significa que uma representação da **String** de todos os tipos baseados em número e em caractere, e uma representação da cadeia de caracteres hexadecimais de colunas binárias, como binary, varbinary, varbinary(max), image, timestamp e uniqueidentifier, podem ser retornadas.  
  
 Os tipos que diferenciam local, como money, smallmoney, datetime, smalldatetime, float, real, decimal e numeric, retornarão o formato toString() canônico para o valor subjacente do tipo.  
  
 Os tipos definidos pelo usuário são retornados como valores de **cadeia de caracteres** hexadecimais.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
