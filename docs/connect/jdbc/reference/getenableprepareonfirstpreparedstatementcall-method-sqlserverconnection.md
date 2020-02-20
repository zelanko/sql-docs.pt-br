---
title: Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac1cf4dbd8c8c14b5c97dbfecbe81d397c1598ce
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983449"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Retorna o valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall**. Se for false, a primeira execução chamará sp_executesql e não preparará uma instrução. Assim que a segunda execução ocorrer, chamará sp_prepexec e configurará efetivamente um identificador de instrução preparada. As execuções subsequentes chamarão sp_execute. Isso elimina a necessidade de sp_unprepare no fechamento da instrução preparada se a instrução é executada apenas uma vez. O padrão para essa opção pode ser alterado chamando setDefaultEnablePrepareOnFirstPreparedStatementCall().

## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Valor retornado
 Um **booliano** que contém o valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall**.

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentários  
 Esse método está disponível no JDBC Driver versão 6.4 e em diante.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
