---
title: Método setObject (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7110f6c5-4af3-4b50-a4d4-1bae1876c70d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdd1912a04c503b59064a0e39859a5845c4c6b0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973306"
---
# <a name="setobject-method-sqlservercallablestatement"></a>Método setObject (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor do parâmetro designado usando o objeto fornecido.  
  
 A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3,0, o comportamento desse método é modificado pela propriedade de conexão **sendTimeAsDatetime** ([definindo as propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte Configurando [como os valores de Java. Sql. time são enviados ao servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nome|Descrição|  
|----------|-----------------|  
|[setObject (java.lang.String, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object.md)|Define o valor do parâmetro designado usando o objeto fornecido.|  
|[setObject (java.lang.String, java.lang.Object, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int.md)|Define o valor do parâmetro designado usando o objeto e o tipo de destino fornecidos.|  
|[setObject (java.lang.String, java.lang.Object, int, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int-int.md)|Define o valor do parâmetro designado usando o objeto, o tipo de destino e a escala fornecidos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
