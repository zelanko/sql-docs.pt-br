---
title: Método getTableName (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getTableName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9a077b50-cc5a-4301-9398-49ea68544e89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b57f01670b52eaa17102001411458153be481f0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979246"
---
# <a name="gettablename-method-sqlserverresultsetmetadata"></a>Método getTableName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém o nome de tabela da coluna designada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getTableName(int column)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *column*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o nome da tabela.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTableName é especificado pelo método getTableName na interface java.sql.ResultSetMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLServerResultSetMetaData Methods](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
