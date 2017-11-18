---
title: "Método getSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs"
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
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 625d1e864cd0f913dbf8826372017ee99a80e41d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>Método getSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esse método foi adicionado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 Retorna a configuração do **sendTimeAsDatetime** propriedade de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se os valores serão enviados ao servidor como um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** tipo. **False** se os valores serão enviados ao servidor como um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **tempo** tipo.  
  
## <a name="remarks"></a>Comentários  
 Consulte [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md) para obter mais informações sobre o **sendTimeAsDatetime** propriedade de conexão.  
  
 [Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) permite que você defina programaticamente o **sendTimeAsDatetime** propriedade de conexão.  
  
 Para obter mais informações, consulte [Java.SQL. time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

