---
title: Método (SQLServerResultSet) isBeforeFirst | Microsoft Docs
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
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1df75b7fd5e0728275b5a431855ffdc3db3d8a10
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="isbeforefirst-method-sqlserverresultset"></a>isBeforeFirst método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se o cursor estiver antes da primeira linha neste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se o cursor estiver antes da primeira linha. **False** se o cursor estiver em qualquer outra posição ou se o conjunto de resultados não contém linhas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isBeforeFirst é especificado pelo método isBeforeFirst na interface Java.SQL. resultset.  
  
 Se esse método for usado com cursores dinâmicos, incluindo cursores somente encaminhamento e somente leitura, e se a propriedade de conexão selectMethod estiver definida como "cursor", ocorrerá uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
