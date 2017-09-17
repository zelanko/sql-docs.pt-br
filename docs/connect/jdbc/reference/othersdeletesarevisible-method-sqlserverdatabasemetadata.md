---
title: "Método othersDeletesAreVisible (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.othersDeletesAreVisible
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4692a8c-e6b7-4edc-9dad-7af816988de5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6a25f8ed48aa924601ce0cf0f603cb0bf18c8af4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="othersdeletesarevisible-method-sqlserverdatabasemetadata"></a>Método othersDeletesAreVisible (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se as exclusões feitas por outros são visíveis.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean othersDeletesAreVisible(int type)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *tipo*  
  
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
  
## <a name="return-value"></a>Valor de retorno  
 **True** se as exclusões estiverem visíveis. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método othersDeletesAreVisible é especificado pelo método othersDeletesAreVisible na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
