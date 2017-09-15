---
title: "Método executeBatch (SQLServerPreparedStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c339a53bd782047db67bc58a61283ce9cd4cbe9e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="executebatch-method-sqlserverpreparedstatement"></a>Método executeBatch (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Uma matriz de ints que contém as contagens de atualização.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Comentários  
 Esse método executeBatch é especificado pelo método executeBatch na interface Java.SQL. Statement.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 está em conformidade com a recomendação do JDBC 4.0 que uma chamada ao método CallableStatement.executeBatch (herdado de PreparedStatement) lançará um BatchUpdateException se o procedimento armazenado aceita OUT ou INOUT parâmetros ou retorna algo diferente de uma contagem de atualização.  
  
 Esse método substitui [Executebatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
