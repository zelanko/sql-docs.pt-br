---
title: "Método Next (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5fe62919bd765d83e2d3a38a9cdda33d88312e29
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="next-method-sqlserverresultset"></a>Método Next (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor uma linha para baixo a partir da posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a nova linha atual for válida. **False** se não existem mais linhas para processar.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método próximo é especificado pelo método na interface Java.SQL. ResultSet Avançar.  
  
 Um cursor de conjunto de resultados é inicialmente posicionado antes da primeira linha. A primeira chamada para o próximo método torna a primeira linha a linha atual, a segunda chamada torna a segunda linha a linha atual e assim por diante.  
  
 Se um fluxo de entrada estiver aberto para a linha atual, uma chamada para o próximo método fechará implicitamente. Uma cadeia de aviso para o [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto é limpo quando uma nova linha é lida.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

