---
description: Método setTime (SQLServerPreparedStatement)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1beac0c34b17e851cbe2a0dbc94445e25a9c8254
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472169"
---
# <a name="settime-method-sqlserverpreparedstatement"></a>Método setTime (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor de tempo fornecido.  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 e versões posteriores, o comportamento desse método foi modificado pela propriedade de conexão **sendTimeAsDatetime** ([Definir as propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para mais informações, confira [Configuração de como os valores de java.sql.Time são enviados ao servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nome|Descrição|  
|----------|-----------------|  
|[setTime (int, java.sql.Time)](../../../connect/jdbc/reference/settime-method-int-java-sql-time.md)|Define o parâmetro designado como o valor de tempo fornecido.|  
|[setTime (int, java.sql.Time, java.util.Calendar)](../../../connect/jdbc/reference/settime-method-int-java-sql-time-java-util-calendar.md)|Define o parâmetro designado como os valores de tempo e calendário fornecidos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
