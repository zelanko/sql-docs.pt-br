---
description: Método prepareStatement (java.lang.String, java.lang.String[])
title: Método prepareStatement (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0db2871-3a5f-4fcc-af61-92333042dcd1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 51c8d9f09419c0d738bc819270c82a43471549be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432888"
---
# <a name="preparestatement-method-javalangstring-javalangstring"></a>Método prepareStatement (java.lang.String, java.lang.String[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) para enviar instruções SQL com parâmetros ao banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sql*  
  
 Uma **String** contendo uma instrução SQL.  
  
 *columnNames*  
  
 Uma matriz de nomes de coluna **String**.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto PreparedStatement.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método prepareStatement é especificado pelo método prepareStatement na interface java.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Método prepareStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
