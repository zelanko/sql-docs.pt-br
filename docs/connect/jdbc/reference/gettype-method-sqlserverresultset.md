---
title: Método (SQLServerResultSet) getType | Microsoft Docs
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
- SQLServerResultSet.getType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffbc4a02-e851-431c-bc1a-7ab381d982bb
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf3e7ea4d8cda491041b3bcd74db10089d52b8a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="gettype-method-sqlserverresultset"></a>getType método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o tipo de cursor deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getType()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o tipo de cursor atual, que pode ser um dos seguintes valores:  
  
 ResultSet.TYPE_FORWARD_ONLY  
  
 ResultSet.TYPE_SCROLL_INSENSITIVE  
  
 ResultSet.TYPE_SCROLL_SENSITIVE  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getType é especificado pelo método na interface Java.SQL. ResultSet getType.  
  
 Esse método pode ser usado para determinar o tipo de curso real. Se o aplicativo selecionou TYPE_FORWARD_ONLY ou usou um tipo de cursor padrão, TYPE_FORWARD_ONLY será retornado.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
