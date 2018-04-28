---
title: Método supportsTransactionIsolationLevel | Microsoft Docs
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
- SQLServerDatabaseMetaData.supportsTransactionIsolationLevel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b716ed6c-6ec3-47a7-8e6d-16cbf2469d6d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ca2e5ea7546da2e214076faa75f70c0da120fd8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="supportstransactionisolationlevel-method-sqlserverdatabasemetadata"></a>Método supportsTransactionIsolationLevel (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte ao nível de isolamento de transação fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsTransactionIsolationLevel(int level)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nível*  
  
 Um **int** que indica o nível de isolamento da transação.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsTransactionIsolationLevel é especificado pelo método supportsTransactionIsolationLevel na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
