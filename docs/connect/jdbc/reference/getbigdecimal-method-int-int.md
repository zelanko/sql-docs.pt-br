---
description: Método getBigDecimal (int, int)
title: Método getBigDecimal (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d9351b35-7046-4852-a612-72d4c46b2bbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bca09005a56846517a70d49d8c846d8d45a45b5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437328"
---
# <a name="getbigdecimal-method-int-int"></a>Método getBigDecimal (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um java.math.BigDecimal, considerando a escala e o índice do parâmetro.  
  
> [!NOTE]  
>  Esse método foi substituído na especificação do JDBC. Em vez disso, você deve usar o método [getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *scale*  
  
 Um **int** que indica o número de dígitos à direita da vírgula decimal.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto BigDecimal.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método getBigDecimal é especificado pelo método getBigDecimal na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBigDecimal &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
