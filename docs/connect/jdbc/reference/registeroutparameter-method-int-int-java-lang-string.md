---
title: Método registerOutParameter (int, int, Java) | Microsoft Docs
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
- SQLServerCallableStatement.registerOutParameter (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3eb5c384-6751-4d50-be23-0c2ccc35593c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0c70c1a7e21fea1c586aa6ef0c3bb3e69229b71
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="registeroutparameter-method-int-int-javalangstring"></a>Método registerOutParameter (int, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra o parâmetro OUT na posição ordinal especificada para o tipo de JDBC e nome do tipo fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 java.lang.String typeName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica a posição ordinal do parâmetro.  
  
 *SQLtype*  
  
 Um código do tipo de JDBC, conforme definido em java.sql.Types.  
  
 *typeName*  
  
 Um **cadeia de caracteres** que contém o nome totalmente qualificado do tipo SQL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método registerOutParameter é especificado pelo método registerOutParameter na interface do CallableStatement.  
  
 Começando com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, quando *sqlType* é de Types. time de tipo, o comportamento desse método é modificado o **sendTimeAsDatetime** propriedade de conexão ([Definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte [Java.SQL. time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
