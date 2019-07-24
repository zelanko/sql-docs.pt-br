---
title: Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce67d0e688ae3ad8909915d9906608f5370830b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983396"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall** . Se essa configuração retornar false, a primeira execução de uma instrução preparada chamará sp_executesql e não preparará uma instrução, depois que a segunda execução ocorrer, chamará sp_prepexec e, na verdade, configurará um identificador de instrução preparado. As execuções a seguir chamarão sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução for executada apenas uma vez. 
  
## <a name="syntax"></a>Sintaxe  
  
```
public boolean getEnablePrepareOnFirstPreparedStatementCall();  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna o **valor** booliano da propriedade de conexão **enablePrepareOnFirstPreparedStatementCall**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método está disponível no JDBC Driver versão 6,4 e em diante.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
