---
title: Método (savepoint) Rollback | Microsoft Docs
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
- SQLServerConnection.rollback (java.sql.Savepoint)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d5dbd9ef-194f-4130-bfcc-7901a4fa8ded
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd3f71c5ecef7962e7dde08efd1c744539883228
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rollback-method-javasqlsavepoint"></a>Método rollback (java.sql.Savepoint)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Desfaz todas as alterações feitas após o determinado [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto foi definido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void rollback(java.sql.Savepoint s)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *S*  
  
 O objeto de ponto de salvamento para reverter para.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método de reversão é especificado pelo método de reversão na interface Java.SQL.  
  
 Esse método deverá ser usado apenas quando o modo de confirmação automática tiver sido desabilitado.  
  
## <a name="see-also"></a>Consulte também  
 [Método Rollback &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
