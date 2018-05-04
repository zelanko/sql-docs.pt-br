---
title: Método getCursorName (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5b3af67-423a-4551-a4c6-a4bc076bd504
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9380759edeb222776f9686c56192b6d1a877ad23
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getcursorname-method-sqlserverresultset"></a>Método getCursorName (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o nome do cursor SQL que é usado por este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
> [!NOTE]  
>  Esse método não é suportado atualmente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Se chamado, uma exceção será lançada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getCursorName()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o nome de cursor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getCursorName é especificado pelo método getCursorName na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
