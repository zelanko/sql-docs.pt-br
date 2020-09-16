---
description: Método getClientConnectionID (SQLServerConnection)
title: Método getClientConnectionID (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 84d4ac45655231430d444781738d47de57f732b8
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480764"
---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>Método getClientConnectionID (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém a ID de conexão da última tentativa de conexão, seja a tentativa bem-sucedida ou não.  
  
## <a name="syntax"></a>Sintaxe  
  
``` 
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um GUID de 16 bytes que representa a ID de conexão da última tentativa de conexão. Ou então, NULL se houver uma falha após a solicitação de conexão ter sido iniciada e houver handshake de pré-logon.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre como acessar informações de diagnóstico no log de eventos estendido, confira [Acessar informações de diagnóstico no Log de Eventos Estendido](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
 O exemplo a seguir mostra como obter a ID de conexão:  
  
```  
Connection con = DriverManager.getConnection(connectionUrl);  
UUID id = ((ISQLServerConnection)con).getClientConnectionId();  
```  
  
 O exemplo abaixo mostra uma outra maneira de obter a ID de conexão:  
  
```  
SQLServerConnectionPoolDataSource ds = new SQLServerConnectionPoolDataSource();  
ds.setUser("...");  
ds.setPassword("...");  
ds.setServerName("...");  
PooledConnection pcon= ds.getPooledConnection();  
Connection cn = pcon.getConnection();  
UUID conid = ((ISQLServerConnection)cn).getClientConnectionId();  
```  
  
 **getClientConnectionID** funciona independentemente da versão do servidor à qual você se conecta, mas os logs de eventos estendidos e a entrada no buffer do anéis de conectividade não estarão presentes no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 R2 e versões anteriores.  
  
 Você também pode localizar a ID de conexão no log de eventos estendidos para verificar se a falha foi no servidor, caso o evento estendido para registro da ID de conexão tiver sido habilitado. Também é possível localizar a ID de conexão no buffer de anéis da conexão ([Solução de problemas de conectividade no SQL Server 2008 com o buffer de anéis de conectividade](https://docs.microsoft.com/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer)) para saber mais sobre certos erros de conexão. Se a ID de conexão não estiver no buffer de anéis da conexão, você pode presumir que houve erro de rede.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
