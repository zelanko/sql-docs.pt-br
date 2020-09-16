---
description: Construtor SQLServerClob (SQLServerConnection, java.lang.String)
title: Construtor SQLServerClob (SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ea4bec9b1d3bc8ab297d548dfb8c94f4007d861
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478588"
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>Construtor SQLServerClob (SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância da classe [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md), quando for fornecido um objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) e uma cadeia de caracteres de dados.  
  
> [!NOTE]  
>  Este método foi substituído no JDBC Driver versão 2.0. Em vez disso, use o método [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) da classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *connection*  
  
 Um objeto SQLServerConnection.  
  
 *data*  
  
 Os dados CLOB.  
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
