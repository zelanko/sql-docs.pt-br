---
title: "Método setObject (Java, java.lang.Object) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.setObject (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 14b84409-5510-4642-a83b-732d8511c5b1
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8c6d664616a000acfb628ebcb15ba1eb917f059
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setobject-method-javalangstring-javalangobject"></a>Método setObject (java.lang.String, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor do parâmetro designado usando o objeto fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setObject(java.lang.String sCol,  
                      java.lang.Object o)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
 *o*  
  
 Um **objeto** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setObject é especificado pelo método setObject na interface do CallableStatement.  
  
 Esse método converte o parâmetro especificado para um CHAR se um NULL for dado, antes de enviá-lo ao banco de dados. Se o parâmetro for declarado como binário, varbinary ou um tipo SQL de imagem, uma exceção será lançada quando a instrução for executada.  
  
 Começando com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, o comportamento desse método é modificado pelo **sendTimeAsDatetime** propriedade de conexão ([definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [ Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte [Java.SQL. time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Método setObject &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
