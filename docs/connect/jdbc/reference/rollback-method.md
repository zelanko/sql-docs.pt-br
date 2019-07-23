---
title: Método Rollback () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.rollback ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7adb6772-4047-4d8e-931d-b3d20eec44b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e3b4575251cb4eb55f9af37bb81ed2c4bedbf564
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975706"
---
# <a name="rollback-method-"></a>Método rollback ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Desfaz todas as alterações feitas na transação atual e libera todos os bloqueios de banco de dados atualmente mantidos pelo objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void rollback()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método rollBack é especificado pelo método rollBack na interface java. Sql. Connection.  
  
 Esse método deverá ser usado apenas quando o modo de confirmação automática tiver sido desabilitado.  
  
## <a name="see-also"></a>Consulte Também  
 [reverter método &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
