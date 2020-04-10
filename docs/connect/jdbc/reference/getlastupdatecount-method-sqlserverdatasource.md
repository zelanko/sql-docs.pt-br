---
title: Método getLastUpdateCount (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e4d5fad788d2a695410035d8689330e25044976
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921404"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>Método getLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um valor **Booliano** que indica se a propriedade lastUpdateCount está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se lastUpdateCount estiver habilitado. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade lastUpdateCount estiver definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] retornará apenas a última contagem de atualização de uma instrução SQL passada ao servidor. Se a propriedade lastUpdateCount estiver definida como **false**, o driver retornará todas as contagens de atualização, inclusive as retornadas por quaisquer gatilhos que tenham disparado. Se a propriedade lastUpdateCount não estiver definida, o método getLastUpdateCount retornará o valor padrão, **true**.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
