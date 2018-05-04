---
title: Método setCursorName (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.setCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3f3ec4f2-103a-4e16-9206-c5bd8639f946
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 432684c052faff1ea79c1976f8c0792be9ec70d5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setcursorname-method-sqlserverstatement"></a>Método setCursorName (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do cursor SQL como a cadeia de caracteres especificada, que será usada por métodos de execução subsequentes.  
  
> [!NOTE]  
>  Esse método não é suportado atualmente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Chamar este método não tem nenhum efeito.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setCursorName(java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *name*  
  
 Um **cadeia de caracteres** que contém o nome de cursor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setCursorName é especificado pelo método setCursorName na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
