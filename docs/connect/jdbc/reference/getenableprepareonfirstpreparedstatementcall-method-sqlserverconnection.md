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
manager: jroth
ms.openlocfilehash: 5d6d755283bddca91661907da5a0709cc71c9368
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767128"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Retorna o valor de **enablePrepareOnFirstPreparedStatementCall** propriedade de conexão. Se for false, a primeira execução chamará sp_executesql e não preparar uma instrução, depois que a segunda execução ocorre, ele será chamar sp_prepexec e configurar, na verdade, um identificador de instrução preparada. Execuções a seguir chamará sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez. O padrão para essa opção pode ser alterado pela chamada setDefaultEnablePrepareOnFirstPreparedStatementCall().

## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Valor retornado
 Um **boolean** que contém o valor de **enablePrepareOnFirstPreparedStatementCall** propriedade de conexão.

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método está disponível na versão do JDBC driver 6.4 e daí.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
