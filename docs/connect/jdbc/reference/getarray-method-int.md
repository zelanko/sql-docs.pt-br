---
title: Método getArray (int) | Microsoft Docs
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
- SQLServerCallableStatement.getArray (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5b839d3f-5a4e-43da-b93c-dc9e0f6d4b3b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e563b5694e770b61191da6444016d30553aa16e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getarray-method-int"></a>Método getArray (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto Array, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Array getArray(int i)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *i*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de matriz.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getArray é especificado pelo método getArray na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método getArray &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
