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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 819c10d0b137d5e0999c1e10bf22810392509f76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288162"
---
# <a name="arguments-in-catalog-functions"></a>Argumentos em funções de catálogo
Todas as funções de catálogo aceitam argumentos com os quais um aplicativo pode restringir o escopo dos dados retornados. Por exemplo, a primeira e segunda chamadas para **SQLTables** no código a seguir retornam um conjunto de resultados que contém informações sobre todas as tabelas, enquanto a terceira chamada retorna informações sobre a tabela Orders:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Os argumentos de cadeia de caracteres de função de catálogo se enquadram em quatro tipos diferentes: argumento comum (OA), argumento de valor de padrão (VP), argumento de identificador (ID) e argumento de lista de valores (VL). A maioria dos argumentos de cadeia de caracteres pode ser de um dos dois tipos diferentes, dependendo do valor do atributo de instrução SQL_ATTR_METADATA_ID. A tabela a seguir lista os argumentos para cada função de catálogo e descreve o tipo do argumento para um valor de SQL_TRUE ou SQL_FALSE de SQL_ATTR_METADATA_ID.  
  
|Função|Argumento|Digite quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Digite quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *schemasname* *TableName* *ColumnName*|OA DE OA DE OA|ID DA ID ID|  
|**SQLColumns**|*CatalogName* *schemasname* *TableName* *ColumnName*|OA PV PV PV|ID DA ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA DE OA DE OA OA DE OA OA|ID ID ID ID ID|  
|**SQLPrimaryKeys**|*Nome_do_catálogo* *SchemaName* *TableName*|OA OA DE OA|ID DA ID DE ID|  
|**SQLProcedureColumns**|*CatalogName* *schemas* - *proc* . *ColumnName*|OA PV PV PV|ID DA ID ID|  
|**SQLProcedures**|*CatalogName* *schemas* *ProcName*|OA PV VP|ID DA ID DE ID|  
|**SQLSpecialColumns**|*Nome_do_catálogo* *SchemaName* *TableName*|OA OA DE OA|ID DA ID DE ID|  
|**SQLStatistics**|*Nome_do_catálogo* *SchemaName* *TableName*|OA OA DE OA|ID DA ID DE ID|  
|**SQLTablePrivileges**|*Nome_do_catálogo* *SchemaName* *TableName*|OA PV VP|ID DA ID DE ID|  
|**SQLTables**|*Nome_do_catálogo* *SchemaName* *TableName* *TableName*|PV PV PV VL|ID DE ID DE ID VL|  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Argumentos comuns](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argumentos do identificador](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumentos da lista de valor](../../../odbc/reference/develop-app/value-list-arguments.md)
