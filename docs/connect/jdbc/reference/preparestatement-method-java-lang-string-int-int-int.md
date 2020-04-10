---
title: Método prepareStatement (java.lang.String, int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b78d2192-f315-4c45-9051-c77059e2c3f4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0629ee8020c6b1be5f8273c16fe814cf05e922b5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924094"
---
# <a name="preparestatement-method-javalangstring-int-int-int"></a>Método prepareStatement (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) que gera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) com o tipo, a simultaneidade e a suspensão fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int nType,  
                                                   int nConcur,  
                                                   int nHold)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sql*  
  
 Uma **String** contendo uma instrução SQL.  
  
 *nType*  
  
 Um **int** que indica o tipo de conjunto de resultados.  
  
 *nConcur*  
  
 Um **int** que indica o tipo de simultaneidade do conjunto de resultados.  
  
 *nHold*  
  
 Um **int** que indica a suspensão do conjunto de resultados.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto PreparedStatement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método prepareStatement é especificado pelo método prepareStatement na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método prepareStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
