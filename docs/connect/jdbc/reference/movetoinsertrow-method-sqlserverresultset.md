---
title: Método (SQLServerResultSet) moveToInsertRow | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3a53a13c1352f33033a9507b66a4b257265acc3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839731"
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
  
## <a name="remarks"></a>Remarks  
 Esse método moveToInsertRow é especificado pelo método moveToInsertRow na interface Java.SQL. resultset.  
  
 A posição do cursor atual será lembrada enquanto o cursor estiver posicionado na linha de inserção. A linha de inserção é uma linha especial associada a um conjunto de resultados atualizável. É essencialmente um buffer onde uma nova linha pode ser construída chamando os métodos updater antes de adicionar a linha ao conjunto de resultados.  
  
 Somente o updater, getter e [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) métodos podem ser chamados quando o cursor estiver na linha de inserção. Todas as colunas em um conjunto de resultados devem ser fornecido um valor de cada vez que esse método é chamado e antes de chamar insertRow. Um método updater deve ser chamado antes que um método getter possa ser chamado em um valor de coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
