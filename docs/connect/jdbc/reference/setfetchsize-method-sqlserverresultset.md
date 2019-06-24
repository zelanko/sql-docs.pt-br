---
title: Método setFetchSize (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5d0bd8714714a479f9370ed2c60b626006e1964
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803379"
---
# <a name="setfetchsize-method-sqlserverresultset"></a>Método setFetchSize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dá ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias para o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *rows*  
  
 Um **int** que indica o número de linhas a serem buscadas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setFetchSize é especificado pelo método setFetchSize na interface do resultset.  
  
 Se o tamanho de busca especificado for zero, o driver JDBC ignorará o valor e estimará qual deve ser o tamanho da busca. O valor padrão é definido pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que criou o conjunto de resultados. O tamanho de busca pode ser alterado a qualquer momento.  
  
 Esse método altera o tamanho de busca de bloqueio para os cursores do servidor e entra em vigor na próxima vez em que o driver JDBC precisar chamar sp_cursorfetch. Ao definir o tamanho de busca para zero, o tamanho de busca padrão para o tipo de cursor atualmente em uso será restaurado  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
