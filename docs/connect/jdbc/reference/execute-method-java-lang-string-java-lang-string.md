---
title: "Método Execute (Java, Java) | Microsoft Docs"
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
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dc327a107a8a164e00f2f34f21515c96766e21d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring-javalangstring"></a>Método Execute (Java, Java)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida, que pode retornar vários resultados e sinaliza [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] que as chaves geradas automaticamente indicadas na matriz fornecida devem ser disponibilizadas para recuperação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *SQL*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
 *columnNames*  
  
 Uma matriz de cadeias de conexão que indica quais nomes de coluna das chave geradas automaticamente devem ser disponibilizados.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se o primeiro resultado é um conjunto de resultados. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método execute é especificado pelo método execute na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Executar método &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

