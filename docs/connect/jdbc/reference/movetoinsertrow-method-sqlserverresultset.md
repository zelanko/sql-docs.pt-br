---
title: "Método (SQLServerResultSet) moveToInsertRow | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSet.moveToInsertRow
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a430421535e5037771256b43353148ae12c35d18
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>moveToInsertRow método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor para a linha de inserção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método moveToInsertRow é especificado pelo método moveToInsertRow na interface Java.SQL. resultset.  
  
 A posição do cursor atual será lembrada enquanto o cursor estiver posicionado na linha de inserção. A linha de inserção é uma linha especial associada a um conjunto de resultados atualizável. É essencialmente um buffer onde uma nova linha pode ser construída chamando os métodos updater antes de adicionar a linha ao conjunto de resultados.  
  
 Somente o updater, getter e [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) métodos podem ser chamados quando o cursor estiver na linha de inserção. Todas as colunas em um conjunto de resultados devem ser fornecido um valor de cada vez que esse método é chamado e antes de chamar insertRow. Um método updater deve ser chamado antes que um método getter possa ser chamado em um valor de coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
