---
title: "Método TRUNCATE (SQLServerNClob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7e8210d-a724-4bae-832a-ae4c63031c9c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8efaadf45586f631572417a364a8009d7d41e3a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="truncate-method-sqlservernclob"></a>Método truncate (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Trunca o **NCLOB** para o comprimento especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Len*  
  
 O comprimento, em caracteres, para que o **NCLOB** valor deve ser truncado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método truncate é especificado pelo método na interface Java.SQL. NCLOB truncar.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

