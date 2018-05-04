---
title: Método getCatalogName (SQLServerResultSetMetaData) | Microsoft Docs
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
- SQLServerResultSetMetaData.getCatalogName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 64f62569-5d8e-411f-a98d-ddc52798391e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88a676981860cd1561c2d785021ecaab3acbe14b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getcatalogname-method-sqlserverresultsetmetadata"></a>Método getCatalogName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém o nome do catálogo da tabela que inclui a coluna designada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getCatalogName(int column)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *column*  
  
 Um **int** que indica o índice da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o nome do catálogo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getCatalogName é especificado pelo método getCatalogName na interface Java.SQL. resultsetmetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros de SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
