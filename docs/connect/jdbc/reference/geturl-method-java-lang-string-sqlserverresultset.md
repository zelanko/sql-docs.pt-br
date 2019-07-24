---
title: Método getURL (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getURL (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 105a5319-0f4c-4d08-964b-cc52f8e28ec1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0407ac8ec711d6d7ab8b1b2fb8afa245f53049d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978325"
---
# <a name="geturl-method-javalangstring-sqlserverresultset"></a>Método getURL (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto URL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.net.URL getURL(java.lang.String sColumn)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sColumn*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto de URL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getURL é especificado pelo método getURL na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método &#40;getURL SQLServerResultSet&#41;](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
