---
title: "Executar método (Java) | Microsoft Docs"
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
- SQLServerPreparedStatement.execute (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a871917e-d286-46c3-96cf-2e8e8b22111c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 219d4ff6ff793b244e30ca43582f4d194e7e6a5d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring"></a>Método execute (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida que pode retornar vários resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *SQL*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a instrução retorna um conjunto de resultados. **False** se ela retorna uma contagem de atualização ou nenhum resultado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método execute é especificado pelo método execute na interface Java.SQL. Statement.  
  
 Esse método substitui o [executar](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) que se encontra no método o [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe.  
  
 Chamar esse método resultará em uma exceção porque a instrução SQL para o objeto SQLServerPreparedStatement for especificada quando o objeto é criado.  
  
## <a name="see-also"></a>Consulte também  
 [Executar método &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

