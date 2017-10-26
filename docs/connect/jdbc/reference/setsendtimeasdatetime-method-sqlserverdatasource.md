---
title: "Método setSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f6a576e4cb3ef155092a1244bbf9e7c2fcaaadd5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>Método setSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esse método foi adicionado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 Modifica a configuração de **sendTimeAsDatetime** propriedade de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sendTimeAsDateTime*  
  
 Um valor booliano. Quando for verdadeiro, faz com que os valores de Java.SQL. time ser enviado ao servidor como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** tipos. Quando for falso, faz com que os valores de Java.SQL. time ser enviado ao servidor como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **tempo** tipos.  
  
## <a name="remarks"></a>Comentários  
 [Getsendtimeasdatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) retorna a configuração do **sendTimeAsDatetime** propriedade de conexão.  
  
 Para obter mais informações sobre o **sendTimeAsDatetime** propriedade de conexão, consulte [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Para obter mais informações, consulte [Java.SQL. time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

