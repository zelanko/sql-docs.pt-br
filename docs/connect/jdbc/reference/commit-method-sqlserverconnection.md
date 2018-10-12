---
title: Método Commit (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6350dc135971f2f7d37154d4728c5d4922954047
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819414"
---
# <a name="commit-method-sqlserverconnection"></a>Método commit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Torna permanentes todas as alterações feitas desde a confirmação ou reversão anterior e libera todos os bloqueios de banco de dados atualmente mantidos pelo objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método commit é especificado pelo método commit na interface java.sql.Connection.  
  
 Esse método deverá ser usado apenas quando o modo de confirmação automática tiver sido desabilitado.  
  
 Observe que esse método irá falhar e lançar uma exceção se o cliente iniciar uma transação manual e, em seguida, por algum motivo o SQL Server reverterá a transação manual. Por exemplo, uma exceção será lançada se o cliente chamar um procedimento armazenado que explicitamente chama ROLLBACK TRANSACTION e, então, o cliente chamará o método commit. Além disso, se o SQL Server gerar um erro de severidade suficiente (16 ou mais alto) para reverter o cliente que iniciou a transação manual, uma chamada subsequente ao método commit lançará uma exceção.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
