---
title: Método deleteRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 987be5ee9fd49385acf02e52108e1e657fbc08a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66786514"
---
# <a name="deleterow-method-sqlserverresultset"></a>Método deleteRow (SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Exclui a linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) e do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
public void deleteRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método deleteRow é especificado pelo método deleteRow na interface do resultset.  
  
 Esse método não pode ser chamado quando o cursor estiver na linha de inserção.  
  
 Quando usar cursores do conjunto de chaves, esse método deixará um intervalo no conjunto de resultados. Você pode testar esse intervalo usando o método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md). Os números de linha das linhas no conjunto de resultados não se alteram.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
