---
description: Método rollback (java.sql.Savepoint)
title: Método rollback (java.sql.Savepoint) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.rollback (java.sql.Savepoint)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d5dbd9ef-194f-4130-bfcc-7901a4fa8ded
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a25a2721efee6586e8571854f2ce6cea8ee8179
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432708"
---
# <a name="rollback-method-javasqlsavepoint"></a>Método rollback (java.sql.Savepoint)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Desfaz todas as alterações feitas depois que o objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) fornecido foi definido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void rollback(java.sql.Savepoint s)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *s*  
  
 O objeto SavePoint a ser revertido.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método rollback é especificado pelo método rollback na interface java.sql.Connection.  
  
 Esse método deverá ser usado apenas quando o modo de confirmação automática tiver sido desabilitado.  
  
## <a name="see-also"></a>Consulte Também  
 [Método rollback &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
