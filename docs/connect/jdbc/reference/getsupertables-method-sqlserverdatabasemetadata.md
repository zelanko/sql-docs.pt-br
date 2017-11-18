---
title: "Método getSuperTables (SQLServerDatabaseMetaData) | Microsoft Docs"
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
apiname:
- SQLServerDatabaseMetaData.getSuperTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 085461de-367b-4832-88aa-010813d2bc41
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ba72e9badc810ad1938c10d3e3ac6ae4f1d5fc8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getsupertables-method-sqlserverdatabasemetadata"></a>Método getSuperTables (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das hierarquias de tabela definidas em um esquema específico no banco de dados em questão.  
  
> [!NOTE]  
>  Esse método não é suportado atualmente com o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Quando usado, este método sempre retornará um conjunto de resultados vazio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getSuperTables(java.lang.String catalog,  
                                         java.lang.String schemaPattern,  
                                         java.lang.String tableNamePattern)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Catálogo*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo.  
  
 *schemaPattern*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema.  
  
 *tableNamePattern*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de tabela.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getSuperTables é especificado pelo método getSuperTables na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

