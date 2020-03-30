---
title: Método addBatch (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.addBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 95924a8b-a43c-4133-aff6-1d712e60e234
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c19e8cd92f7ee7aafcf6dd23e9c179f2557e628f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67955995"
---
# <a name="addbatch-method-sqlserverstatement"></a>Método addBatch (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Adiciona o comando SQL fornecido à lista atual de comandos do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void addBatch(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sql*  
  
 Uma **String** que contém uma instrução SQL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método addBatch é especificado pelo método addBatch na interface java.sql.Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
