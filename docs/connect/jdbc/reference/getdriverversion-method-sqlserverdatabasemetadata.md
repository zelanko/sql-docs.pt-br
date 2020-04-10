---
title: Método getDriverVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDriverVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3be84d65-af61-4c34-b052-74a5d488eaa9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1066be205916f23747da8fdd61a3ebf0784742ad
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902092"
---
# <a name="getdriverversion-method-sqlserverdatabasemetadata"></a>Método getDriverVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número de versão do driver JDBC em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getDriverVersion()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém a versão do driver JDBC.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getDriverVersion é especificado pelo método getDriverVersion na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
