---
title: Método nativeSQL (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.nativeSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2188a6e1-792f-47bd-b207-1d01741231b2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0f7c55a61d440e3991f74388c9a96be09430f2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="nativesql-method-sqlserverconnection"></a>Método nativeSQL (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Converte a instrução SQL fornecida na gramática SQL nativa do servidor de banco de dados.  
  
> [!NOTE]  
>  Esse método não é suportado atualmente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String nativeSQL(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sql*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém a instrução SQL convertida.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método nativeSQL é especificado pelo método nativeSQL na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
