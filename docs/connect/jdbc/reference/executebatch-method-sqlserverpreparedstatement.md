---
title: Método executeBatch (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b9295a2b82892d570bde1d13ee3fefe81b8a83d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executebatch-method-sqlserverpreparedstatement"></a>Método executeBatch (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Uma matriz de ints que contém as contagens de atualização.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Remarks  
 Esse método executeBatch é especificado pelo método executeBatch na interface Java.SQL. Statement.  
    
 Esse método substitui [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
