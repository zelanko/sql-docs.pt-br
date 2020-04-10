---
title: Método prepareCall (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c6f1b51509f73858093c2d208cf2c9012fb219d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923153"
---
# <a name="preparecall-method-javalangstring-int-int"></a>Método prepareCall (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) que gera os objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) com tipo e simultaneidade fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sql*  
  
 Uma **String** contendo uma instrução SQL.  
  
 *resultSetType*  
  
 Um **int** que indica o tipo de conjunto de resultados.  
  
 *resultSetConcurrency*  
  
 Um **int** que indica o tipo de simultaneidade do conjunto de resultados.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto CallableStatement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método prepareCall é especificado pelo método prepareCall na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método prepareCall &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
