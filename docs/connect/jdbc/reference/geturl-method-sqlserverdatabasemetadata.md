---
description: Método getURL (SQLServerDatabaseMetaData)
title: Método getURL (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7371c5aa585c7ffc9ec434e8c0dbc5ae6ecc4d89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433868"
---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>Método getURL (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a URL do banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém a URL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getURL é especificado pelo método getURL na interface java.sql.DatabaseMetaData.  
  
 Durante o uso do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] com um banco de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], esse método retorna um valor **String** que contém as seguintes informações:  
  
-   Um valor de URL "jdbc:sqlserver://"  
  
-   Propriedades de conexão opcionais, como **ServerName**, **InstanceName**e **PortNumber**  
  
-   As outras propriedades de conexão são definidas pelo usuário e todas as propriedades de conexão com valores padrão de driver não vazios ou não nulos, exceto **userName**, **password** e **integratedSecurity**.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
