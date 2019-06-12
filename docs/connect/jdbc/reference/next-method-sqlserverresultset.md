---
title: Método Next (SQLServerResultSet) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 8fcd3125f45622ddd167acf06ed91ccffb02a3b5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779532"
---
# <a name="next-method-sqlserverresultset"></a>Método next (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor uma linha para baixo a partir da posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se a nova linha atual é válida. **False** se não houver nenhum mais linhas a serem processadas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método next é especificado pelo método next na interface java.sql.ResultSet.  
  
 Um cursor de conjunto de resultados é inicialmente posicionado antes da primeira linha. A primeira chamada ao método next torna a primeira linha a linha atual, a segunda chamada torna a segunda linha a linha atual, e assim por diante.  
  
 Se um fluxo de entrada estiver aberto para a linha atual, uma chamada ao método next o fechará implicitamente. Uma cadeia de avisos para o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) é removida quando uma nova linha é lida.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
