---
title: Método relative (SQLServerResultSet) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f9233d6e4224e33d9d9c71b1352a792ba19cff2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80904032"
---
# <a name="relative-method-sqlserverresultset"></a>Método relative (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor de acordo com um número de linhas fornecido em relação à linha atual, em uma direção positiva ou negativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *nRows*  
  
 Um **int** que indica o número de linhas a serem movidas.  
  
## <a name="return-value"></a>Valor retornado  
 **true** se o cursor estiver em uma linha. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método relative é especificado pelo método relative na interface java.sql.ResultSet.  
  
 Ao tentar se mover além da primeira ou última linha no conjunto de resultados, o cursor será posicionado antes ou depois da primeira ou última coluna. Chamar `relative(0)` é válido, mas não altera a posição do cursor.  
  
 Chamar o método `relative(1)` é exatamente igual a chamar o método [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md). Chamar o método `relative(-1)` é exatamente igual a chamar o método [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
