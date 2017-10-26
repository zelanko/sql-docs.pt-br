---
title: "Método getClientConnectionID (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b422c085307db5630cb1b70a47cafd935877dcd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>Método getClientConnectionID (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém a ID de conexão da última tentativa de conexão, seja a tentativa bem-sucedida ou não.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um GUID de 16 bytes que representa a ID de conexão da última tentativa de conexão. Ou então, NULL se houver uma falha após a solicitação de conexão ter sido iniciada e houver handshake de pré-logon.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre como acessar informações de diagnóstico no log de eventos estendidos, consulte [acessando informações de diagnóstico no Log de eventos estendidos](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
 O exemplo a seguir mostra como obter a ID de conexão:  
  
```  
Connection con = DriverManager.getConnection(connectionUrl);  
UUID id = ((ISQLServerConnection)con).getClientConnectionId();  
```  
  
 O exemplo abaixo mostra uma outra maneira de obter a ID de conexão:  
  
```  
SQLServerConnectionPoolDataSource ds = new SQLServerConnectionPoolDataSource();  
ds.setUser("…");  
ds.setPassword("…");  
ds.setServerName("…");  
PooledConnection pcon= ds.getPooledConnection();  
Connection cn = pcon.getConnection();  
UUID conid = ((ISQLServerConnection)cn).getClientConnectionId();  
```  
  
 **getClientConnectionID** funciona independentemente de qual versão do servidor de você se conectar, mas os logs de eventos estendidos e entrada sobre os erros de buffer de anéis de conectividade não estarão presentes no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 2008 R2 e versões anteriores.  
  
 Você também pode localizar a ID de conexão no log de eventos estendidos para verificar se a falha foi no servidor, caso o evento estendido para registro da ID de conexão tiver sido habilitado. Também é possível localizar a ID de conexão no buffer de anéis de conexão ([solução de problemas de conectividade no SQL Server 2008 com o Buffer de anéis de conectividade](http://go.microsoft.com/fwlink/?LinkId=207752)) para certos erros de conexão. Se a ID de conexão não estiver no buffer de anéis da conexão, você pode presumir que houve erro de rede.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

