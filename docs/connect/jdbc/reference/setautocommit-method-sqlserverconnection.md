---
title: "Método (SQLServerConnection) setAutoCommit | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1549693ac6b4e558c2fc86b29dc6aaa6122c235
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# setAutoCommit método (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o modo de confirmação automática para este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto para o estado especificado.  
  
## Sintaxe  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### Parâmetros  
 *value*  
  
 **True** para habilitar o modo de confirmação automática para a conexão, **false** para desabilitá-lo.  
  
## Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Comentários  
 Esse método setAutoCommit é especificado pelo método setAutoCommit na interface Java.SQL.  
  
 Se uma conexão estiver no modo de confirmação automática, todas as suas instruções SQL serão executadas e confirmadas como transações individuais. Caso contrário, suas instruções SQL são agrupadas em transações que são terminadas por uma chamada para o [confirmação](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) método ou o [reversão](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md) método. Por padrão, as novas conexões estão no modo de confirmação automática.  
  
 A confirmação ocorre quando a instrução é concluída ou a próxima execução ocorre, o que ocorrer primeiro. No caso de instruções que retornam um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) do objeto, a instrução é concluída quando a última linha do conjunto de resultados foi recuperada ou quando o conjunto de resultados foi fechado. Em casos avançados, uma única instrução pode retornar vários resultados além dos valores de parâmetro de saída. Nesses casos, a confirmação ocorrerá quando todos os resultados e valores de parâmetro de saída tiverem sido recuperados.  
  
 Quando o modo de confirmação automática é **false**, o driver JDBC implicitamente iniciará uma nova transação após cada confirmação.  
  
> [!NOTE]  
>  Se esse método for chamado durante uma transação, esta será confirmada.  
  
## Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

