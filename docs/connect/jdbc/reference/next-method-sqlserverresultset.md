---
title: Método next (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c83fe6aa33d77db98fcdfc757b9bf219a45a9b15
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976762"
---
# <a name="next-method-sqlserverresultset"></a>Método next (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor uma linha para baixo a partir da posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se a nova linha atual for válida. **false** se não houver mais linhas a processar.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método next é especificado pelo método next na interface java.sql.ResultSet.  
  
 Um cursor de conjunto de resultados é inicialmente posicionado antes da primeira linha. A primeira chamada ao método next torna a primeira linha a linha atual, a segunda chamada torna a segunda linha a linha atual, e assim por diante.  
  
 Se um fluxo de entrada estiver aberto para a linha atual, uma chamada ao método next o fechará implicitamente. Uma cadeia de avisos para o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) é removida quando uma nova linha é lida.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
