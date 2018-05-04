---
title: Executar método (Java) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.execute (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a871917e-d286-46c3-96cf-2e8e8b22111c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 595091b5ce933cb53e0f3de90a12f3ec621e8111
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="execute-method-javalangstring"></a>Método execute (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida que pode retornar vários resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sql*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a instrução retorna um conjunto de resultados. **False** se ela retorna uma contagem de atualização ou nenhum resultado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método execute é especificado pelo método execute na interface Java.SQL. Statement.  
  
 Esse método substitui o método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) que é localizado na classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
 Chamar esse método resultará em uma exceção, uma vez que a instrução SQL para o objeto SQLServerPreparedStatement é especificada quando o objeto é criado.  
  
## <a name="see-also"></a>Consulte também  
 [Método execute &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
