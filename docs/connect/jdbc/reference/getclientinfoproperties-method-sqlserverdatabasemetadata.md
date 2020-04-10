---
title: Método getClientInfoProperties (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a84002f7b44644ee5ba86ee277925e5f482b412
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926001"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>Método getClientInfoProperties (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma lista das propriedades de informações de cliente que têm o suporte do driver.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto ResultSet.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getClientInfoProperties é especificado pelo método getClientInfoProperties na interface java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  Esse método retorna um conjunto de resultados vazio. O driver dá suporte apenas à configuração **applicationName** e define o **applicationName** somente em tempo de conexão. O SQL Server não dá suporte à atualização das informações de aplicativo cliente depois que a conexão é estabelecida.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
