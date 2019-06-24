---
title: Método setTime com valor de tempo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTime (java.lang.String, java.lang.Time)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49301bec-6cf2-43fb-9d4e-e3986164a208
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 80c0b7027f9d2ffe3d5afea7d70a3e8929ee3fc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66791688"
---
# <a name="settime-method-javalangstring-javasqltime"></a>Método setTime (java.lang.String, java.sql.Time)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor de tempo fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTime(java.lang.String sCol,  
                    java.sql.Time t)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *t*  
  
 Um objeto de tempo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setTime é especificado pelo método setTime na interface java.sql.CallableStatement.  
  
 Começando com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0, o comportamento desse método é modificado pela **sendTimeAsDatetime** propriedade de conexão ([definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [ Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte [time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método setTime &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
