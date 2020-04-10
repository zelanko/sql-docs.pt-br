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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5e9b17bed19df5f08d35a8d69b85c839ced215b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922013"
---
# <a name="executequery-method-sqlserverstatement"></a>Método executeQuery (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida e retorna um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sql*  
  
 Uma **String** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeQuery é especificado pelo método executeQuery na interface java.sql.Statement.  
  
 [O SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) é gerado se a instrução SQL fornecida produz algo diferente de um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) .  
  
 Se a execução de um procedimento armazenado resultar em uma contagem de atualização maior que um, ou que gere mais de um conjunto de resultados, use o método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para executar o procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
