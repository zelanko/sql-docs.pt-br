---
title: "Método prepareStatement (Java, Java) | Microsoft Docs"
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
apiname:
- SQLServerConnection.prepareStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0db2871-3a5f-4fcc-af61-92333042dcd1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db68fda928104c6e6f143e2042af58dd8198d4fe
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="preparestatement-method-javalangstring-javalangstring"></a>Método prepareStatement (Java, Java)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) parametrizadas de objeto para enviar instruções SQL para o banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *SQL*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
 *columnNames*  
  
 Um **cadeia de caracteres** matriz de nomes de coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto PreparedStatement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método prepareStatement é especificado pelo método prepareStatement na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Método prepareStatement &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

