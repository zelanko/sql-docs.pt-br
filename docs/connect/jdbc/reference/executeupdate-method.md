---
title: "Método executeUpdate () | Microsoft Docs"
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
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1bbfe020096bba2cec77907d97e36918684894d6
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-"></a>Método executeUpdate ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL na [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) do objeto, que deve ser um SQL INSERT, UPDATE, MERGE ou DELETE instrução; ou uma instrução SQL que não retorne nada, como uma instrução DDL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número de linhas afetadas ou 0 se usando uma instrução DDL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeUpdate é especificado pelo método na interface PreparedStatement executeUpdate.  
  
## <a name="see-also"></a>Consulte também  
 [Método executeUpdate &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

