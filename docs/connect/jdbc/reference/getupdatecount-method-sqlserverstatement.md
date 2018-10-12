---
title: Método getUpdateCount (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c4dadcaa4bfb0c2bf4698cf7b4e0be02a7d4ccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633734"
---
# <a name="getupdatecount-method-sqlserverstatement"></a>Método getUpdateCount (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o resultado atual como uma contagem de atualização.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que contém a contagem de atualização. Se o resultado retornado for um objeto do conjunto de resultados ou não houver mais resultados, será retornado o valor -1.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getUpdateCount é especificado pelo método getUpdateCount na interface Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
