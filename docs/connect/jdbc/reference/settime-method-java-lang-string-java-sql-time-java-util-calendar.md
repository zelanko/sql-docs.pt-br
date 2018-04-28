---
title: Método setTime para valores de hora e calendário | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerCallableStatement.setTime (java.lang.String, java.lang.Time, java.lang.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca08fea8-ee1a-49e4-a973-2923d325df79
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ebc9cbefff5dbb741bb9755bd5a57f9350259e6c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="settime-method-javalangstring-javasqltime-javautilcalendar"></a>Método setTime (java.lang.String, java.sql.Time, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como os valores de tempo e calendário fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTime(java.lang.String sCol,  
                    java.sql.Time x,  
                    java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
 *x*  
  
 Um objeto de tempo.  
  
 *c*  
  
 Um objeto de calendário.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setTime é especificado pelo método setTime na interface do CallableStatement.  
  
 Começando com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, o comportamento desse método é modificado pelo **sendTimeAsDatetime** propriedade de conexão ([definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [ Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte [Java.SQL. time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Método setTime &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
