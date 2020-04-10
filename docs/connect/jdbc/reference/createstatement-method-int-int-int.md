---
title: Método createStatement (int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: adf3e74fc6fe823d816e3f86993fe9075d966289
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927675"
---
# <a name="createstatement-method-int-int-int"></a>Método createStatement (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que gera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) com tipo, simultaneidade e suspensão fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *resultSetType*  
  
 O valor **int** que representa o tipo de conjunto de resultados.  
  
 *nConcur*  
  
 O valor **int** que representa o tipo de simultaneidade de conjunto de resultados.  
  
 *nHold*  
  
 O valor **int** que representa a suspensão.  
  
## <a name="return-value"></a>Valor retornado  
 O objeto Statement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método createStatement é especificado pelo método createStatement na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
