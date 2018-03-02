---
title: "setEnablePrepareOnFirstPreparedStatementCall método (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea672e1cd3b5998ca6829fb0f4c9fae29773d9d2
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
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
  
  
