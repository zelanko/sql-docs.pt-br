---
title: Método getColumnName (SQLServerResultSetMetaData) | Microsoft Docs
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
- SQLServerResultSetMetaData.getColumnName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0330ca1d-5e24-4ce3-9d2a-b931f20a0fcf
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 089170607395e99a39749fe58cf69dd88afe39c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getcolumnname-method-sqlserverresultsetmetadata"></a>Método getColumnName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém o nome da coluna designada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getColumnName(int column)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *column*  
  
 Um **int** que indica o índice da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getColumnName é especificado pelo método getColumnName na interface Java.SQL. resultsetmetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros de SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
