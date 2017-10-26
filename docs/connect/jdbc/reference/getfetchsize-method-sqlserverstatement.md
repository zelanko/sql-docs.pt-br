---
title: "Método (SQLServerStatement) getFetchSize | Microsoft Docs"
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
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: efb6e1aca84c36afbfb761813ae8ab0efdfd2501
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize método (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número de resultado de conjunto de linhas que é o tamanho da busca padrão para objetos gerado neste conjunto de resultados [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o tamanho da busca, que é especificado pelo [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) método.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getFetchSize é especificado pelo método getFetchSize na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

