---
title: "Método getLoginTimeout (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba6f8e0a85aba2afbc8cdae99b7cca76d749352b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>Comentários  
 Se o aplicativo não especificar um valor de tempo limite explicitamente, este método retornará um valor padrão de 15 segundos.  
  
 Esse método getLoginTimeout é especificado pelo método getLoginTimeout na interface javax.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

