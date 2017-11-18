---
title: "Método getClientInfoProperties (SQLServerDatabaseMetaData) | Microsoft Docs"
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
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 022f09c50d0a47851e375fcbb617ee40266dbb38
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>Método getClientInfoProperties (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma lista das propriedades de informações de cliente que têm o suporte do driver.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de conjunto de resultados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getClientInfoProperties é especificado pelo método getClientInfoProperties na interface DatabaseMetadata.  
  
> [!NOTE]  
>  Esse método retorna um conjunto de resultados vazio. O driver dá suporte apenas a configuração de **applicationName** e define o **applicationName** somente em tempo de conexão. O SQL Server não dá suporte à atualização das informações de aplicativo cliente depois que a conexão é estabelecida.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

