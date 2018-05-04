---
title: Classe SQLServerXAConnection | Microsoft Docs
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
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba48701c441a75f0d7c6b7f78c964384c47f94e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Remarks  
 Um objeto SQLServerXAConnection pode ser inscrita em uma transação distribuída por meio de um [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) objeto. Um Gerenciador de transações, normalmente parte de um servidor de camada intermediária, gerencia um objeto SQLServerXAConnection por meio do objeto SQLServerXAResource.  
  
> [!NOTE]  
>  Os programadores de aplicativo normalmente não usam essa interface diretamente. Ela é usada principalmente por um gerenciador de transações que funciona no servidor de camada intermediária.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
