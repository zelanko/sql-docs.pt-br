---
title: Método Relative (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b8907a5e2eb2ead5202e8aec9fd5320a6047a5f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797710"
---
# <a name="relative-method-sqlserverresultset"></a>Método relative (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor de acordo com um número de linhas fornecido em relação à linha atual, em uma direção positiva ou negativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nRows*  
  
 Um **int** que indica o número de linhas a serem movidas.  
  
## <a name="return-value"></a>Valor retornado  
 **True** se o cursor estiver em uma linha. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método relativo é especificado pelo método na interface do ResultSet relativo.  
  
 Ao tentar se mover além da primeira ou última linha no conjunto de resultados, o cursor será posicionado antes ou depois da primeira ou última coluna. Chamar `relative(0)` é válido, mas não altera a posição do cursor.  
  
 Chamar o método `relative(1)` é exatamente igual a chamar o método [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md). Chamar o método `relative(-1)` é exatamente igual a chamar o método [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
