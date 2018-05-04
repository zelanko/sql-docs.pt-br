---
title: setEnablePrepareOnFirstPreparedStatementCall método (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d06aaf8ce55583c11e7503dae2810220b1797f2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>setEnablePrepareOnFirstPreparedStatementCall método (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Especifica o comportamento de uma instância de conexão específica. Se o valor for false, a primeira execução será chamada sp_executesql e não prepara uma instrução, depois que a segunda execução acontece ele chamar sp_prepexec e configurar, na verdade, um identificador de instrução preparada. A seguir execuções chamará sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.

## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 O novo valor da **enablePrepareOnFirstPreparedStatementCall** propriedade de conexão.  
 
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
