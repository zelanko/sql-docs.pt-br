---
title: Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf48b4d280e9205a72025a346495f83aca68a064
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922395"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Especifica o comportamento de uma instância de conexão específica. Se o valor for false, a primeira execução chamará sp_executesql e não preparará uma instrução. Assim que a segunda execução ocorrer, chamará sp_prepexec e configurará efetivamente um identificador de instrução preparada. As execuções subsequentes chamarão sp_execute. Isso elimina a necessidade de sp_unprepare no fechamento da instrução preparada se a instrução é executada apenas uma vez.

## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 O novo valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall**.  
 
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentários  
 Esse método está disponível no driver JDBC versão 6.4 e posteriores.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
