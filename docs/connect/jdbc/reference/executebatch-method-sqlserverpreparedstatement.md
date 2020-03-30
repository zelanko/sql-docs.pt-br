---
title: Método executeBatch (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 463106c14a63feddb68998affff8131933e81dfa
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954894"
---
# <a name="executebatch-method-sqlserverpreparedstatement"></a>Método executeBatch (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma matriz de ints que contém as contagens de atualização.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Comentários  
 Esse método executeBatch é especificado pelo método executeBatch na interface java.sql.Statement.  
    
 Esse método substitui [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
