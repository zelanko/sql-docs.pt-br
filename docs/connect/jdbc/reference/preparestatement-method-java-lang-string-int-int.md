---
description: Método prepareStatement (java.lang.String, int, int)
title: Método prepareStatement (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5bb96dbe-f673-41b5-911b-8f661cca071a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9cbb24ea7e33779665b80a8a967f739df4b74baa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432908"
---
# <a name="preparestatement-method-javalangstring-int-int"></a>Método prepareStatement (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) que gera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) com o tipo e a simultaneidade fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sSql,  
                                                   int resultSetType,  
                                                   int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sSql*  
  
 Uma **String** contendo uma instrução SQL.  
  
 *resultSetType*  
  
 Um **int** que indica o tipo de conjunto de resultados.  
  
 *resultSetConcurrency*  
  
 Um **int** que indica o tipo de simultaneidade do conjunto de resultados.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto PreparedStatement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método prepareStatement é especificado pelo método prepareStatement na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-methods.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
