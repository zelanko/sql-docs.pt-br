---
title: Método getCatalogTerm (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0aa5d372-16aa-4790-a8f6-f8b742798f8f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c0c718524b8800df02625e6392de1f9d4600291
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953320"
---
# <a name="getcatalogterm-method-sqlserverdatabasemetadata"></a>Método getCatalogTerm (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o termo preferencial do fornecedor de banco de dados para "catalog".  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getCatalogTerm()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o termo do catálogo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método getCatalogTerm é especificado pelo método getCatalogTerm na interface java.sql.DatabaseMetaData.  
  
 Quando o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] é usado com um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método retorna o termo "database".  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
