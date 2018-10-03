---
title: Método isBeforeFirst (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77ff7c0808f2d6e53fc15814612352abe3ad2479
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783904"
---
# <a name="isbeforefirst-method-sqlserverresultset"></a>Método isBeforeFirst (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se o cursor está antes da primeira linha no objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se o cursor antes da primeira linha. **False** se o cursor estiver em nenhuma outra posição ou se o conjunto de resultados não contém linhas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isBeforeFirst é especificado pelo método isBeforeFirst na interface do resultset.  
  
 Se esse método for usado com cursores dinâmicos, incluindo cursores somente encaminhamento e somente leitura, e se a propriedade de conexão selectMethod estiver definida como "cursor", ocorrerá uma exceção.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
