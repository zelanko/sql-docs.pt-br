---
description: Método getAttributes (SQLServerDatabaseMetaData)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca2ee077821ace1f5661d7764f80a70177717300
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437358"
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
  
#### <a name="parameters"></a>parâmetros  
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
  
## <a name="remarks"></a>Comentários  
 Esse método getAttributes é especificado pelo método getAttributes na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
