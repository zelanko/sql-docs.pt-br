---
title: Método setLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a242499204215f0d8ecdb16698bcc0fe07377db3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794263"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>Método setLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número de segundos que este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) aguardará enquanto tenta estabelecer uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *loginTimeout*  
  
 Um valor **int** que representa o número de segundos de espera. Zero indica que o tempo limite é o padrão do sistema, especificado como 15 segundos por padrão.  
  
## <a name="remarks"></a>Remarks  
 Esse método setLoginTimeout é especificado pelo método setLoginTimeout na interface javax.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
