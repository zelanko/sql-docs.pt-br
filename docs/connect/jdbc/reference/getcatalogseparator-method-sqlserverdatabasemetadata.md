---
title: "Método getCatalogSeparator (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getCatalogSeparator
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0bbd6842-7210-432a-bef4-e15a63f5cc96
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5531ae6c62a8e0a588abc136a09e15171074013
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getcatalogseparator-method-sqlserverdatabasemetadata"></a>Método getCatalogSeparator (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o **cadeia de caracteres** que usa esse banco de dados como o separador entre um nome de catálogo e da tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getCatalogSeparator()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o separador de catálogo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getCatalogSeparator é especificado pelo método getCatalogSeparator na interface DatabaseMetadata.  
  
 Ao usar o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] com um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados, este método retorna um ponto (".") como o separador de catálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
