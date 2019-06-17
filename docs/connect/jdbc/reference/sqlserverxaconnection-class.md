---
title: Classe SQLServerXAConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 177b10c9657c4cb8d6b37f7dec9d3b860308dcb7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788899"
---
# <a name="sqlserverxaconnection-class"></a>Classe SQLServerXAConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa conexões JDBC que podem participar de transações distribuídas (XA).  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **Implementa:** javax.sql.XAConnection  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>Remarks  
 Um objeto SQLServerXAConnection pode ser inscrito em uma transação distribuída por meio de um objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md). Um Gerenciador de transações, normalmente parte de um servidor de camada intermediária, gerencia um objeto SQLServerXAConnection por meio do objeto SQLServerXAResource.  
  
> [!NOTE]  
>  Os programadores de aplicativo normalmente não usam essa interface diretamente. Ela é usada principalmente por um gerenciador de transações que funciona no servidor de camada intermediária.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
