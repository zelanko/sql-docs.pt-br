---
title: Método setLoginTimeout (SQLServerDataSource) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08aa17692a03f444a304e65b6ae7ad2f872ff34a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>Método setLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número de segundos que isso [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto aguardará ao tentar estabelecer uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *LoginTimeout*  
  
 Um **int** valor que representa o número de segundos de espera. Zero indica que o tempo limite é o padrão do sistema, especificado como 15 segundos por padrão.  
  
## <a name="remarks"></a>Remarks  
 Esse método setLoginTimeout é especificado pelo método setLoginTimeout na interface javax.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
