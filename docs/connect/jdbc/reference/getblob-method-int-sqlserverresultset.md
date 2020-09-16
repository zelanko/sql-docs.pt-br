---
description: Método getBlob (int) (SQLServerResultSet)
title: Método getBlob (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBlob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a00275cb-0299-4a21-a518-2640598a5bbf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ada62df07595c44e3552f44fc4d36a6d5065ce7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437148"
---
# <a name="getblob-method-int-sqlserverresultset"></a>Método getBlob (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do índice da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto Blob na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Blob getBlob(int i)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *i*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto Blob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBlob é especificado pelo método getBlob na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBlob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
