---
title: Método getDatabaseMinorVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDatabaseMinorVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18163668-60d6-4d54-aaf1-c338b8c90f2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f0dc89feb46c0210a07730e00cda84e3008387e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923222"
---
# <a name="getdatabaseminorversion-method-sqlserverdatabasemetadata"></a>Método getDatabaseMinorVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número da versão secundária do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getDatabaseMinorVersion()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica a versão secundária do banco de dados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getDatabaseMinorVersion é especificado pelo método getDatabaseMinorVersion na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
