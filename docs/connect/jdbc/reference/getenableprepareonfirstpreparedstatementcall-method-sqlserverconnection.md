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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983449"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Retorna o valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall** . Se false, a primeira execução chamará sp_executesql e não preparará uma instrução, assim que a segunda execução ocorrer, chamará sp_prepexec e, na verdade, configurará um identificador de instrução preparado. As execuções a seguir chamarão sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução for executada apenas uma vez. O padrão para essa opção pode ser alterado chamando setDefaultEnablePrepareOnFirstPreparedStatementCall ().

## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Valor retornado
 Um **booliano** que contém o valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall** .

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método está disponível no JDBC Driver versão 6,4 e em diante.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
