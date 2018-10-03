---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0372cab3f29733306262e7986d2dd8e407e78564
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47768604"
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
  
## <a name="remarks"></a>Remarks  
 Esse método getURL é especificado pelo método getURL na interface java.sql.DatabaseMetaData.  
  
 Durante o uso do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] com um banco de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], esse método retorna um valor **String** que contém as seguintes informações:  
  
-   Um valor de URL "jdbc:sqlserver://"  
  
-   Propriedades de conexão opcionais, como **nome_do_servidor**, **instanceName**, e **portNumber**  
  
-   As outras propriedades de conexão são definidas pelo usuário e todas as propriedades de conexão com valores padrão de driver não vazios ou não nulos, exceto **userName**, **password** e **integratedSecurity**.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
