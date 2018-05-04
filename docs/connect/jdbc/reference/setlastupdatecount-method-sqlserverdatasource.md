---
title: Método setLastUpdateCount (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: feab7a78a4aa8fd89d5cedfca14be1246923d948
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>Método setLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define uma **booliano** valor que indica se a propriedade lastUpdateCount está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *lastUpdateCount*  
  
 **True** se lastUpdateCount estiver habilitada. Caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade lastUpdateCount estiver definida como **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] retornará apenas a última contagem de atualização de uma instrução SQL passada para o servidor. Se a propriedade lastUpdateCount estiver definida como **false**, o driver retornará todas as contagens, inclusive as retornadas por gatilhos que tenham disparado de atualização. Se a propriedade lastUpdateCount não estiver definida, o [getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) método retorna o valor padrão de **true**.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
