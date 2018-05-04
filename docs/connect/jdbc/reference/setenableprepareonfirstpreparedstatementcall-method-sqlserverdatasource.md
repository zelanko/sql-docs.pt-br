---
title: setEnablePrepareOnFirstPreparedStatementCall método (SQLServerDataSource) | Microsoft Docs
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
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92f7148fa5d79ca7743d33c423a23e5ab6367958
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>setEnablePrepareOnFirstPreparedStatementCall método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Especifica o comportamento de uma instância de conexão específica. Se essa configuração for false, a primeira execução de uma instrução preparada será chamada sp_executesql e não prepara uma instrução, depois que a segunda execução acontece ele chamar sp_prepexec e instalação, na verdade, um identificador de instrução preparada. A seguir execuções chamará sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.  
## <a name="syntax"></a>Sintaxe  
  
```
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 O novo valor da **enablePrepareOnFirstPreparedStatementCall** propriedade de conexão.  

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
