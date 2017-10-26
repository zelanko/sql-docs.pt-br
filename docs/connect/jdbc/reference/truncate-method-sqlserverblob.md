---
title: "Método TRUNCATE (SQLServerBlob) | Microsoft Docs"
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
- SQLServerBlob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ef181e04-003a-442a-9b7e-0c508a7cc873
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e1e04414b9ecda98f1275846fae29f009490a53b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="truncate-method-sqlserverblob"></a>Método truncate (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Trunca um BLOB, considerando o comprimento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Len*  
  
 O novo comprimento do BLOB.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método truncate é especificado pelo método truncate na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

