---
title: Método getRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a266e3bc-05c2-44e2-9346-125ae6780216
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4c9d83bbdb3f724c7d28d3881e7f27c1c0f70584
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980280"
---
# <a name="getrow-method-sqlserverresultset"></a>Método getRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número da linha atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getRow()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número da linha atual; 0 se não houver nenhuma linha.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getRow é especificado pelo método getRow na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
