---
title: Método registerOutParameter (int, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3eb5c384-6751-4d50-be23-0c2ccc35593c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bf855697561638c0d4ca560c345bf2d21e4b027
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975914"
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
  
 *sqlType*  
  
 Um código do tipo de JDBC, conforme definido em java.sql.Types.  
  
 *typeName*  
  
 Uma **String** que contém o nome do tipo SQL totalmente qualificado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método registerOutParameter é especificado pelo método registerOutParameter na interface java. Sql. CallableStatement.  
  
 A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3,0, quando *SqlType* é do tipo Java. Sql. Types. time, o comportamento desse método é modificado pela propriedade de conexão **sendTimeAsDatetime** ([definindo as propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [ SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte Configurando [como os valores de Java. Sql. time são enviados ao servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
