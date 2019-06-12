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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 99d01841ca24cc1a7e34864b42018dac51fa1861
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768224"
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
  
#### <a name="parameters"></a>Parâmetros  
 *resultSetType*  
  
 O valor **int** que representa o tipo de conjunto de resultados.  
  
 *nConcur*  
  
 O valor **int** que representa o tipo de simultaneidade de conjunto de resultados.  
  
 *nHold*  
  
 O valor **int** que representa a suspensão.  
  
## <a name="return-value"></a>Valor retornado  
 O objeto de instrução.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método prepareStatement é especificado pelo método prepareStatement na interface do Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
