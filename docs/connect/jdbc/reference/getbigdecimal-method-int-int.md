---
title: "Método getBigDecimal (int, int) | Microsoft Docs"
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
- SQLServerCallableStatement.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d9351b35-7046-4852-a612-72d4c46b2bbb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 492e404743fdcd43b08f08fbdbcccb51810a30f3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getbigdecimal-method-int-int"></a>Método getBigDecimal (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um java.math.BigDecimal, considerando a escala e o índice do parâmetro.  
  
> [!NOTE]  
>  Esse método foi substituído na especificação do JDBC. Em vez disso, você deve usar o [getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *índice*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *scale*  
  
 Um **int** que indica o número de dígitos à direita da vírgula decimal.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto BigDecimal.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBigDecimal é especificado pelo método getBigDecimal na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método getBigDecimal &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

