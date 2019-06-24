---
title: Método getSchemaTerm (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemaTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3e4a400f-0859-4ac3-983e-c25633b33683
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f90f44319777ce0554f9fa4feeb66dc8af6b9162
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66792058"
---
# <a name="getschematerm-method-sqlserverdatabasemetadata"></a>Método getSchemaTerm (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o termo preferencial para "esquema" no banco de dados em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getSchemaTerm()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o termo preferencial.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getSchemaTerm é especificado pelo método getSchemaTerm na interface java.sql.DatabaseMetaData.  
  
 Quando o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] é usado com um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método retorna "schema" como o termo preferencial.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
