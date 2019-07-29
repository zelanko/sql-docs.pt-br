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
ms.openlocfilehash: bc02d31a1d13a3d32f581da6fb3367473cb88bbb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955135"
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
 Esse método deleteRow é especificado pelo método deleteRow na interface java. Sql. ResultSet.  
  
 Esse método não pode ser chamado quando o cursor estiver na linha de inserção.  
  
 Quando usar cursores do conjunto de chaves, esse método deixará um intervalo no conjunto de resultados. Você pode testar esse intervalo usando o método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md). Os números de linha das linhas no conjunto de resultados não se alteram.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
