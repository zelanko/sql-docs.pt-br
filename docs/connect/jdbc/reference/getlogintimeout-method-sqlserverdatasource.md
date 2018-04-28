---
title: Método getLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ca310bbfa7b367f595ecf35ef92e9189ef323a0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>Método getLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o número de segundos que este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto aguardará ao tentar estabelecer uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** valor que representa o número de segundos de espera.  
  
## <a name="remarks"></a>Remarks  
 Se o aplicativo não especificar um valor de tempo limite explicitamente, este método retornará um valor padrão de 15 segundos.  
  
 Esse método getLoginTimeout é especificado pelo método getLoginTimeout na interface javax.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
