---
title: Classe SQLServerConnectionPoolDataSource | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82712fa541d958527c409d5a347b69f37d5e642f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource Class
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa conexões de banco de dados físicas para gerentes de pool de conexões.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **Implementa:** javax.SQL. connectionpooldatasource  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>Comentários  
 SQLServerConnectionPoolDataSource normalmente é usado em ambientes de Java Application Server que suportam pool de conexão interna e exigem um ConnectionPoolDataSource fornecer conexões físicas, como a plataforma Java, Enterprise Edition (Java Servidores de aplicativos EE) que fornece a API do JDBC 3.0 o pool de conexão da especificação.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

