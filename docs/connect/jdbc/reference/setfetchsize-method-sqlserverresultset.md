---
title: Método (SQLServerResultSet) setFetchSize | Microsoft Docs
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
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32e6999e9cdfadb8ca05bba46325ee722cbc6fd5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32843183"
---
# <a name="setfetchsize-method-sqlserverresultset"></a>setFetchSize método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dá ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas forem necessárias para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *rows*  
  
 Um **int** indicando o número de linhas a serem buscadas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setFetchSize é especificado pelo método setFetchSize na interface Java.SQL. resultset.  
  
 Se o tamanho de busca especificado for zero, o driver JDBC ignorará o valor e estimará qual deve ser o tamanho da busca. O valor padrão é definido [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que criou o conjunto de resultados. O tamanho de busca pode ser alterado a qualquer momento.  
  
 Esse método altera o tamanho de busca de bloqueio para os cursores do servidor e entra em vigor na próxima vez em que o driver JDBC precisar chamar sp_cursorfetch. Ao definir o tamanho de busca para zero, o tamanho de busca padrão para o tipo de cursor atualmente em uso será restaurado  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
