---
title: Argumentos em funções de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5dd36e82b71ff862a543bfa38cda4b4a660738a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789314"
---
# <a name="arguments-in-catalog-functions"></a>Argumentos em funções de catálogo
Todas as funções de catálogo aceitam argumentos com os quais um aplicativo pode restringir o escopo dos dados retornados. Por exemplo, as primeiros e segunda chamadas para **SQLTables** no código a seguir retornam um conjunto de resultados contendo informações sobre todas as tabelas, enquanto a terceira chamada retorna informações sobre a tabela de pedidos:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Argumentos de cadeia de caracteres da função de catálogo se enquadram em quatro tipos diferentes: argumento comum (OA), argumento de valor padrão (PV), o argumento de identificador (ID) e o argumento de lista de valor (VL). A maioria dos argumentos de cadeia de caracteres pode ser de um dos dois tipos diferentes, dependendo do valor do atributo de instrução SQL_ATTR_METADATA_ID. A tabela a seguir lista os argumentos para cada função de catálogo e descreve o tipo do argumento para um valor SQL_TRUE ou SQL_FALSE de SQL_ATTR_METADATA_ID.  
  
|Função|Argumento|Digite quando SQL _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Digite quando SQL _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID DE IDENTIFICAÇÃO DE ID DE ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID DE IDENTIFICAÇÃO DE ID DE ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName*  *FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID DE IDENTIFICAÇÃO DE ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID DE IDENTIFICAÇÃO DE ID DE ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|VP DE PV OA|ID DE IDENTIFICAÇÃO DE ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID DE IDENTIFICAÇÃO DE ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID DE IDENTIFICAÇÃO DE ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|VP DE PV OA|ID DE IDENTIFICAÇÃO DE ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|VP PV PV VL|ID ID ID VL|  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Argumentos comuns](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argumentos do identificador](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumentos da lista de valor](../../../odbc/reference/develop-app/value-list-arguments.md)
