---
title: Método (Java) getRef | Microsoft Docs
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
- SQLServerCallableStatement.getRef (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a8ff2dd5-923b-4a2f-ab33-665574b2dfda
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c00b4e58d5b98c6a2f5f59cd7dbd0cb8912dc53b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getref-method-javalangstring"></a>Método getRef (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto de referência na linguagem de programação Java considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Ref getRef(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de referência.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getRef é especificado pelo método getRef na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método getRef &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
