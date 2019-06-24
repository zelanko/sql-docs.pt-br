---
title: Método getAttributes (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getAttributes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4dc784ed-4699-4197-9af5-6e03da80d14c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcd33cbb39286c03b5b809b847a8d8a2b8b609f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799960"
---
# <a name="getattributes-method-sqlserverdatabasemetadata"></a>Método getAttributes (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição do atributo especificado do tipo fornecido, para um tipo definido pelo usuário que está disponível no esquema e no catálogo fornecidos.  
  
> [!NOTE]  
>  No momento, este método não é compatível com [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Se for chamado, sempre retornará um conjunto de resultados vazio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getAttributes(java.lang.String catalog,  
                                        java.lang.String schemaPattern,  
                                        java.lang.String typeNamePattern,  
                                        java.lang.String attributeNamePattern)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schemaPattern*  
  
 Uma **String** que contém o padrão de nome do esquema.  
  
 *typeNamePattern*  
  
 Uma **String** que contém o padrão de nome de tipo.  
  
 *attributePattern*  
  
 Uma **String** que contém o padrão de nome de atributo.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getAttributes é especificado pelo método getAttributes na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
