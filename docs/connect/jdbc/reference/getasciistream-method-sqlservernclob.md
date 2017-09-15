---
title: "Método getAsciiStream (SQLServerNClob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ff1d47e4-572a-4169-a631-ac261f7642b3
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9221c48404601029f6ecd16741b9dbf240b719e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getasciistream-method-sqlservernclob"></a>Método getAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o **NCLOB** valor designado por este **NClob** objeto como um fluxo ASCII.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto InputStream que contém os dados NCLOB.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getAsciiStream é especificado pelo método na interface java.sql.SQLServerNClob getAsciiStream.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
