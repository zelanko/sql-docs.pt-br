---
title: Método getRef (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getRef (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 83c60c5d-7a69-498b-be9c-bbdbfafec157
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fbb9a65610730ba23e157aabf81c04c1f4af8eec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980579"
---
# <a name="getref-method-javalangstring-sqlserverresultset"></a>Método getRef (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto Ref na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Ref getRef(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *colName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Ref.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getRef é especificado pelo método getRef na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getRef &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
