---
title: Método getLastUpdateCount (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2582e7764231ef3d12a07d2490643d5c71d07dbc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>Método getLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um **booliano** valor que indica se a propriedade lastUpdateCount está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se lastUpdateCount estiver habilitada. Caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade lastUpdateCount estiver definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] retornará apenas a última contagem de atualização de uma instrução SQL passada para o servidor. Se a propriedade lastUpdateCount estiver definida como **false**, o driver retornará todas as contagens, inclusive as retornadas por gatilhos que tenham disparado de atualização. Se a propriedade lastUpdateCount não estiver definida, o método getLastUpdateCount retornará o valor padrão de **true**.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
