---
title: Método setLastUpdateCount (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: edc0b28c132e5422c12ae340e35c1464ee48fa73
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799253"
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>Método setLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **Booliano** que indica se a propriedade lastUpdateCount está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *lastUpdateCount*  
  
 **True** se lastUpdateCount está habilitada. Caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade lastUpdateCount estiver definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] retornará apenas a última contagem de atualização de uma instrução SQL passada ao servidor. Se a propriedade lastUpdateCount estiver definida como **false**, o driver retornará todas as contagens de atualização, inclusive as retornadas por quaisquer gatilhos que tenham disparado. Se a propriedade lastUpdateCount não estiver definida, o método [getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) retornará o valor padrão, **true**.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
