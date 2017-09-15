---
title: "Método (SQLServerConnection) Commit | Microsoft Docs"
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
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf9cc3b66c0d8b5e9eca015dd5e62fdd7541a9c2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="commit-method-sqlserverconnection"></a>confirmação de método (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Faz com que todas as alterações feitas desde a confirmação ou reversão anterior permanentes e libera todos os bloqueios de banco de dados atualmente mantidos por este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método de confirmação é especificado pelo método de confirmação na interface Java.SQL.  
  
 Esse método deverá ser usado apenas quando o modo de confirmação automática tiver sido desabilitado.  
  
 Observe que esse método irá falhar e lançar uma exceção se o cliente iniciar uma transação manual e, em seguida, por algum motivo o SQL Server reverterá a transação manual. Por exemplo, uma exceção será lançada se o cliente chama um procedimento armazenado que explicitamente chama ROLLBACK TRANSACTION e, em seguida, o cliente chama o método commit. Além disso, se o SQL Server gera um erro de severidade suficiente (16 ou superior) para reverter o cliente iniciou a transação manual; uma chamada subsequente para o método commit lançará uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
