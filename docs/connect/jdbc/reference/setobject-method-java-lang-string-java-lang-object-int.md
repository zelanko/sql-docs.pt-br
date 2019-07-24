---
title: Método setObject (java.lang.String, java.lang.Object, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setObject (java.lang.String, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a9a0c802-7851-4826-b173-87b0c0acb3a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d680bc3ee42be70ec8f8445967599550ebbec2d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973356"
---
# <a name="setobject-method-javalangstring-javalangobject-int"></a>Método setObject (java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor do parâmetro designado usando o objeto e o tipo de destino fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setObject(java.lang.String sCol,  
                      java.lang.Object o,  
                      int n)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *o*  
  
 Um valor **Object**.  
  
 *n*  
  
 Um **int** que indica o tipo de destino conforme definido em java.sql.Types.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setObject é especificado pelo método setObject na interface java.sql.CallableStatement.  
  
 A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3,0, o comportamento desse método é modificado pela propriedade de conexão **sendTimeAsDatetime** ([definindo as propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte Configurando [como os valores de Java. Sql. time são enviados ao servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método setObject &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
