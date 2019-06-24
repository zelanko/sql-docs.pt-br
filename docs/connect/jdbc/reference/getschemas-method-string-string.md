---
title: Método getSchemas (String, String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b4129ebee2be0ca043be349dc57ca8612ab7d0b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66792189"
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
 *catalog*  
  
 O nome de um catálogo no banco de dados. Se for uma cadeia de caracteres vazia "", o resultado incluirá os esquemas sem um catálogo. Se for **null**, o nome do catálogo não será usado para pesquisa.  
  
 *schemaPattern*  
  
 O nome de um esquema. Se for **null**, o nome do esquema não será usado para pesquisa.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getSchemas é especificado pelo método getSchemas na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getSchemas contém as seguintes informações:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**String**|O nome do esquema.|  
|TABLE_CATALOG|**String**|O nome de catálogo para o esquema.|  
  
 Os resultados são ordenados por TABLE_CATALOG e, em seguida, por TABLE_SCHEM. Cada linha tem TABLE_SCHEM como a primeira coluna e TABLE_CATALOG como a segunda coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
