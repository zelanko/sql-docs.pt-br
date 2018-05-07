---
title: Método supportsResultSetConcurrency (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsResultSetConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f7573b2-ac5c-4721-8a02-4b6cb60c74b2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 87b9db3f492cdb0399396b35a15a665be1d6cc49
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supportsresultsetconcurrency-method-sqlserverdatabasemetadata"></a>Método supportsResultSetConcurrency (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte ao tipo de simultaneidade fornecido em combinação com o tipo do conjunto de resultados fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsResultSetConcurrency(int type,  
                                            int concurrency)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *type*  
  
 Um **int** que indica o conjunto de resultados tipo, que pode ser um dos seguintes valores conforme definido em Java.SQL. ResultSet ou SQLServerResultSet:  
  
## <a name="javasqlresultset-types"></a>Tipos java.sql.ResultSet  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>Tipos SQLServerResultSet  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
 *simultaneidade*  
  
 Um **int** que indica o resultado de definir o nível de simultaneidade, que pode ser um dos seguintes valores conforme definido em Java.SQL. ResultSet ou SQLServerResultSet:  
  
## <a name="javasqlresultset-types"></a>Tipos java.sql.ResultSet  
 CONCUR_READ_ONLY  
  
 CONCUR_UPDATABLE  
  
## <a name="sqlserverresultset-types"></a>Tipos SQLServerResultSet  
 CONCUR_SS_OPTIMISTIC_CC  
  
 CONCUR_SS_SCROLL_LOCKS  
  
 CONCUR_SS_OPTIMISTIC_VAL  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsResultSetConcurrency é especificado pelo método supportsResultSetConcurrency na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
