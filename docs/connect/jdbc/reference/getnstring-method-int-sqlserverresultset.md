---
title: Método getNString (int) (SQLServerResultSet) | Microsoft Docs
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
ms.assetid: c8cc4636-01e9-4dc8-a40c-728337ca08f5
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a90e7c76d7bd1c975e9c0a3f1885bdc9c6f29f94
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getnstring-method-int-sqlserverresultset"></a>Método getNString (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor da coluna designada na linha atual do [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto de cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getNString(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de cadeia de caracteres.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getNString é especificado pelo método na interface java.sql.SQLServerResultSet getNString.  
  
 Esse método pode ser usado para recuperar o valor de um **nvarchar**, **nchar**, **nvarchar (max)**, **ntext**, ou **xml** coluna na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto. Se você tentar usar esse método para recuperar valores de outros tipos de dados, uma exceção será lançada.  
  
## <a name="see-also"></a>Consulte também  
 [Método getNString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
