---
title: Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource) | Microsoft Docs
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
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8323c328938188b16d56f9dfa05c3dfd2be16c75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Usado para permitir transações XA estritamente acopladas, que possuem diferentes IDs de transação de ramificação XA (XIDs), mas que têm a mesma ID de transação global (GTRID).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>Valor do campo  
 Um **int** valor de 32768.  
  
## <a name="remarks"></a>Remarks  
 Cada transação é identificada por uma ID de transação de filial XA (XID) e uma ID de transação global (GTRID). Para permitir que os aplicativos usem transações XA firmemente acopladas que possuam XIDs diferentes, mas têm o mesmo GTRID, você deve definir o [SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) no parâmetro do método XAResource.start sinalizadores. Para obter mais informações sobre como usar esse sinalizador, consulte [Noções básicas sobre as transações XA](../../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Campos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
