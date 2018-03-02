---
title: "setDisableStatementPooling método (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
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
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7588e8fc59067a604c977f940f7f7a3e39d20d73
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="setdisablestatementpooling-method-sqlserverdatasource"></a>setDisableStatementPooling método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor da **disableStatementPooling** propriedade de conexão. Se for false, permite que a instrução pool para ser usado em acoplamento com statementPoolingCacheSize valor > 0.  

## <a name="syntax"></a>Sintaxe  
  
```
public void setDisableStatementPooling(boolean disableStatementPooling);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *disableStatementPooling*  
  
 O novo valor da **disableStatementPooling** propriedade de conexão.  

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método é disponível na versão do driver JDBC 6.4 e daí.
 
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
