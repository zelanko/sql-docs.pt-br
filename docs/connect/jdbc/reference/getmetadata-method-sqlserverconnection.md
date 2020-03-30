---
title: Método getMetaData (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getMetaData
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86223cb5-3bf4-489a-8c82-669a91764f2b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4fdf49c68acd2ef1b1544ad02efcb4079ceeac67
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981876"
---
# <a name="getmetadata-method-sqlserverconnection"></a>Método getMetaData (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um objeto [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) que contém metadados sobre o banco de dados para o qual o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) representa uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.DatabaseMetaData getMetaData()  
```  
  
## <a name="return-value"></a>Valor retornado  
 O objeto DatabaseMetaData.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getMetaData é especificado pelo método getMetaData na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
