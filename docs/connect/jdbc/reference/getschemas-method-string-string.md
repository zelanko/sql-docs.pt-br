---
title: "Método (String, String) getSchemas | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1309f95e5ccdb95c6cfe2f60fe88bf6b26794fdf
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="getschemas-method-string-string"></a>Método getSchemas (String, String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera os nomes de esquemas que estão disponíveis no banco de dados atual usando o nome de catálogo especificado e o nome de esquema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public ResultSet getSchemas(java.lang.String catalog,  
                       java.lang.String schemaPattern)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Catálogo*  
  
 O nome de um catálogo no banco de dados. Se for uma cadeia de caracteres vazia "", o resultado incluirá os esquemas sem um catálogo. Se for **nulo**, o nome do catálogo não é usado para pesquisa.  
  
 *schemaPattern*  
  
 O nome de um esquema. Se for **nulo**, o nome do esquema não é usado para pesquisa.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getSchemas é especificado pelo método getSchemas na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getSchemas contém as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**Cadeia de caracteres**|O nome do esquema.|  
|TABLE_CATALOG|**Cadeia de caracteres**|O nome de catálogo para o esquema.|  
  
 Os resultados são ordenados por TABLE_CATALOG e, em seguida, por TABLE_SCHEM. Cada linha tem TABLE_SCHEM como a primeira coluna e TABLE_CATALOG como a segunda coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
