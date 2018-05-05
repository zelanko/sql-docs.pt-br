---
title: Método supportsSubqueriesInQuantifieds (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSubqueriesInQuantifieds
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6749e14c-0f8a-4f1f-8583-dd5cc79b24fe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf7c6ea684d437e3bf271943325e1292a23cf31e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supportssubqueriesinquantifieds-method-sqlserverdatabasemetadata"></a>Método supportsSubqueriesInQuantifieds (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte a subconsultas em expressões quantificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsSubqueriesInQuantifieds()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsSubqueriesInQuantifieds é especificado pelo método supportsSubqueriesInQuantifieds na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
