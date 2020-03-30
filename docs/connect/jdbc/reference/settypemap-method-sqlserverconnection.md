---
title: Método setTypeMap (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setTypeMap
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bffd20a6-1310-44b0-9602-974500481fa6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a188d5d98aca0418a2452f29912f62604f3ffa90
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972176"
---
# <a name="settypemap-method-sqlserverconnection"></a>Método setTypeMap (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Instala o objeto TypeMap fornecido como o mapa de tipo do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.  
  
> [!NOTE]  
>  No momento, este método não é compatível com [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTypeMap(java.util.Map map)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *map*  
  
 Um objeto TypeMap.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setTypeMap é especificado pelo método setTypeMap na interface javax.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
