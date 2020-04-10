---
title: Método getSuperTypes (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSuperTypes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5b8e78e6-2bb0-4dc7-9c77-a5609654cb05
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5c8d9c6c0b4d59aff90515818c13e849a55a1b8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926160"
---
# <a name="getsupertypes-method-sqlserverdatabasemetadata"></a>Método getSuperTypes (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das hierarquias de tipos definidos pelo usuário em um esquema específico no banco de dados em questão.  
  
> [!NOTE]  
>  Esse método não tem suporte no momento com o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Quando usado, este método sempre retornará um conjunto de resultados vazio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getSuperTypes(java.lang.String catalog,  
                                        java.lang.String schemaPattern,  
                                        java.lang.String typeNamePattern)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *catalog*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schemaPattern*  
  
 Uma **String** que contém o padrão de nome do esquema.  
  
 *tableNamePattern*  
  
 Uma **String** que contém o padrão de nome de tabela.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getSuperTypes é especificado pelo método getSuperTypes na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
