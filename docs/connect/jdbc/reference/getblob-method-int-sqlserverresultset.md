---
title: Método getBlob (int) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getBlob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a00275cb-0299-4a21-a518-2640598a5bbf
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e91191de371f196e09241bb604907ae4b0edf2cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getblob-method-int-sqlserverresultset"></a>Método getBlob (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do índice de coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto de Blob na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Blob getBlob(int i)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Eu*  
  
 Um **int** que indica o índice da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de Blob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBlob é especificado pelo método getBlob na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método getBlob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
