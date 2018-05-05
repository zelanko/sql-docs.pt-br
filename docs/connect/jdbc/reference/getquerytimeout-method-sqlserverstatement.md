---
title: Método getQueryTimeout (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.getQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8dff954f-b458-4fa6-abe6-be62ff75e2b9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d644c22ae53308753a473ec0b14289b49eafccbc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getquerytimeout-method-sqlserverstatement"></a>Método getQueryTimeout (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número de segundos [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aguardará para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto a ser executado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getQueryTimeout()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número de segundos que o driver JDBC esperará, ou 0 se não houver nenhum limite.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getQueryTimeout é especificado pelo método getQueryTimeout na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
