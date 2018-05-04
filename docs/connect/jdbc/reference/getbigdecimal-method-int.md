---
title: Método getBigDecimal (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal Method (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f74030d8-3789-463b-b414-2eb01cef8a30
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dc9f4e32e750217e345a74600bac1e186532849
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getbigdecimal-method-int"></a>Método getBigDecimal (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como java.math.BigDecimal com precisão total, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto BigDecimal.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBigDecimal é especificado pelo método getBigDecimal na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método getBigDecimal &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
