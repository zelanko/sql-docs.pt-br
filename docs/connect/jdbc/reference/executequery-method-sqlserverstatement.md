---
title: Método executeQuery (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeQuery
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 599cf463-e19f-4baa-bacb-513cad7c6cd8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8755695a805684338378efa4427c24c333c3da08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796941"
---
# <a name="executequery-method-sqlserverstatement"></a>Método executeQuery (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida e retorna um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sql*  
  
 Uma **String** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método executeQuery é especificado pelo método executeQuery na interface java.sql.Statement.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) será lançada se a instrução SQL fornecida produz algo diferente de uma única [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
 Se a execução de um procedimento armazenado resultar em uma contagem de atualização maior que um, ou que gere mais de um conjunto de resultados, use o método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para executar o procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
