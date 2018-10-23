---
title: Membros SQLServerXAResource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9d55da45733e15a9b2aa98f7c6d8fa386b1e4e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682684"
---
# <a name="sqlserverxaresource-members"></a>Membros SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|Usado para permitir transações XA estritamente acopladas, que possuem diferentes IDs de transação de ramificação XA (XIDs), mas que têm a mesma ID de transação global (GTRID).|  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN, TMFAIL, TMJOIN, TMNOFLAGS, TMONEPHASE, TMRESUME, TMSTARTRSCAN, TMSUCCESS, TMSUSPEND, XA_OK, XA_RDONLY|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|Confirma a transação global especificada pelo objeto Xid fornecido.|  
|[end](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|Termina o trabalho executado em nome de uma ramificação de transação.|  
|[forget](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|Informa ao gerenciador de recursos para esquecer uma ramificação de transação concluída de modo heurístico.|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|Obtém o valor de tempo limite da transação atual para o objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|Determina se a instância do gerenciador de recursos representada pelo objeto de destino é igual à instância do gerenciador de recursos representada pelo objeto XAResource fornecido.|  
|[prepare](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|Solicita que o gerenciador de recursos prepare-se para uma confirmação da transação especificada pelo objeto Xid fornecido.|  
|[recuperação](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|Obtém uma lista de ramificações de transação preparadas de um gerenciador de recursos.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|Solicita que o gerenciador de recursos reverta o trabalho feito em nome de uma ramificação de transação.|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|Define o valor de tempo limite da transação atual para este objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).|  
|[start](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|Inicia o trabalho em nome de um branch de transação especificado no objeto Xid.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
