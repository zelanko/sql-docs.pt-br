---
description: Método findColumn (SQLServerResultSet)
title: Método findColumn (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.findColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c29994a-0b53-420b-8a9b-82a9eef08587
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6fb05e1d128abfb4d81c20081ff458254aa5c09
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437578"
---
# <a name="findcolumn-method-sqlserverresultset"></a>Método findColumn (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o índice da primeira coluna correspondente para o nome de coluna fornecido no objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int findColumn(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Uma **String** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o índice de coluna.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método findColumn é especificado pelo método findColumn na interface java.sql.ResultSet.  
  
 Se houver várias colunas com o mesmo nome, o método findColumn retornará a primeira correspondência com diferenciação de maiúsculas e minúsculas. Se não houver nenhuma correspondência com diferenciação de maiúsculas e minúsculas, esse método retornará a primeira correspondência sem diferenciação de maiúsculas e minúsculas.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
