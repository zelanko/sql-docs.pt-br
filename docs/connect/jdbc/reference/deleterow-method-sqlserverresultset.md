---
title: Método deleteRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
manager: craigg
ms.openlocfilehash: 466fa86609ba4f784e78ba9ac0fb5178d827645e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784114"
---
# <a name="deleterow-method-sqlserverresultset"></a>Método deleteRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Exclui a linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) e do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void deleteRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método deleteRow é especificado pelo método deleteRow na interface do resultset.  
  
 Esse método não pode ser chamado quando o cursor estiver na linha de inserção.  
  
 Ao usar cursores do conjunto de chaves, esse método deixará um buraco no conjunto de resultados. Você pode testar esse buraco usando o método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md). Os números de linha das linhas no conjunto de resultados não se alteram.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
