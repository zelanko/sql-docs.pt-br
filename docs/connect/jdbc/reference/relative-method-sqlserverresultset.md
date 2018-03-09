---
title: "Método Relative (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSet.relative
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c6d936c5e44996a56ac6d9c653cc25ba7176aa4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="relative-method-sqlserverresultset"></a>Método Relative (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor de acordo com um número de linhas fornecido em relação à linha atual, em uma direção positiva ou negativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nRows*  
  
 Um **int** que indica o número de linhas a serem movidas.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se o cursor estiver em uma linha. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método relativo é especificado pelo método na interface Java.SQL. ResultSet relativo.  
  
 Ao tentar se mover além da primeira ou última linha no conjunto de resultados, o cursor será posicionado antes ou depois da primeira ou última coluna. Chamando `relative(0)` é válido, mas não altera a posição do cursor.  
  
 Chamar o método `relative(1)` é idêntico ao chamar o [próximo](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) método. Chamar o método `relative(-1)` é idêntico ao chamar o [anterior](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
