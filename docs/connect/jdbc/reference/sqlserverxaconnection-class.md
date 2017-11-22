---
title: Classe SQLServerXAConnection | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6c016a665405a50ce133de5e45ef77ddf0981d0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverxaconnection-class"></a>Classe SQLServerXAConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa conexões JDBC que podem participar de transações distribuídas (XA).  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **Implementa:** javax.SQL. xaconnection  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>Comentários  
 Um objeto SQLServerXAConnection pode ser inscrita em uma transação distribuída por meio de um [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) objeto. Um Gerenciador de transações, normalmente parte de um servidor de camada intermediária, gerencia um objeto SQLServerXAConnection por meio do objeto SQLServerXAResource.  
  
> [!NOTE]  
>  Os programadores de aplicativo normalmente não usam essa interface diretamente. Ela é usada principalmente por um gerenciador de transações que funciona no servidor de camada intermediária.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
