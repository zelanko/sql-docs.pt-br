---
title: "Método (SQLServerStatement) isPoolable | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 29c948e99dcb9411a427e96c1a9a0492c2d8992f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ispoolable-method-sqlserverstatement"></a>isPoolable método (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um valor que indica se uma instrução pode ser adicionada ao pool de instruções fornecido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a instrução pode ser adicionada ao pool de instruções fornecido pelo usuário; **false** caso contrário.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md) altera o comportamento em um pool de um objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

