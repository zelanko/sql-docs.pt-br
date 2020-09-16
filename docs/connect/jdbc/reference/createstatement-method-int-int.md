---
description: Método createStatement (int, int)
title: Método createStatement (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fda0c8b6055cca6692c37596872c3c7ebae12f81
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437928"
---
# <a name="createstatement-method-int-int"></a>Método createStatement (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que gera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) com o tipo e a simultaneidade fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *resultSetType*  
  
 O valor **int** que representa o tipo do conjunto de resultados.  
  
 *resultSetConcurrency*  
  
 O valor **int** que representa o tipo de simultaneidade do conjunto de resultados.  
  
## <a name="return-value"></a>Valor de retorno  
 O objeto Statement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método createStatement é especificado pelo método createStatement na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
