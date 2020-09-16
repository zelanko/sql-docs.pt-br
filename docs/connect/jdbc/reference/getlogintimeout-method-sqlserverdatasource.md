---
description: Método getLoginTimeout (SQLServerDataSource)
title: Método getLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d1a868a7fc9f562496037dd4280de91aac28b335
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435728"
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>Método getLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o número de segundos que o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) em questão aguardará ao tentar fazer uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **int** que representa o número de segundos de espera.  
  
## <a name="remarks"></a>Comentários  
 Se o aplicativo não especificar um valor de tempo limite explicitamente, este método retornará um valor padrão de 15 segundos.  
  
 Esse método getLoginTimeout é especificado pelo método getLoginTimeout na interface javax.sql.DataSource.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
