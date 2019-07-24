---
title: Método setTime (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTime
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3a83ea3-6636-4096-842b-71b37340fa07
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4b11b2d25abec8717604948101ca81d651fe822
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972453"
---
# <a name="settime-method-sqlserverpreparedstatement"></a>Método setTime (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor de tempo fornecido.  
  
 A partir do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3,0, o comportamento desse método é modificado pela propriedade de conexão **sendTimeAsDatetime** ([definindo as propriedades de conexã](../../../connect/jdbc/setting-the-connection-properties.md)o) e  [SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte Configurando [como os valores de Java. Sql. time são enviados ao servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nome|Descrição|  
|----------|-----------------|  
|[setTime (int, java.sql.Time)](../../../connect/jdbc/reference/settime-method-int-java-sql-time.md)|Define o parâmetro designado como o valor de tempo fornecido.|  
|[setTime (int, java.sql.Time, java.util.Calendar)](../../../connect/jdbc/reference/settime-method-int-java-sql-time-java-util-calendar.md)|Define o parâmetro designado como os valores de tempo e calendário fornecidos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
