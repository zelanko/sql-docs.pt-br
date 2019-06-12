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
manager: jroth
ms.openlocfilehash: 13dd4f2bd18ef3bde6b920be0e5e562dc9aef956
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773806"
---
# <a name="getstring-method-javalangstring-sqlserverresultset"></a>Método getString (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como uma **String** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getString(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor de **String**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getLong é especificado pelo método getLong na interface java.sql.ResultSet.  
  
 Todas as colunas no SQL Server podem ser retornadas como uma String. Isso significa que uma representação da **String** de todos os tipos baseados em número e em caractere, e uma representação da cadeia de caracteres hexadecimais de colunas binárias, como binary, varbinary, varbinary(max), image, timestamp e uniqueidentifier, podem ser retornadas.  
  
 Os tipos que diferenciam local, como money, smallmoney, datetime, smalldatetime, float, real, decimal e numeric, retornarão o formato toString() canônico para o valor subjacente do tipo.  
  
 Os tipos definidos pelo usuário são retornados como valores de **cadeia de caracteres** hexadecimais.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
