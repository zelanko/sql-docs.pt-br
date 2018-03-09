---
title: "Argumentos em funções de catálogo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb973a525b5a978d16566edc02fb4d4651e11406
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="arguments-in-catalog-functions"></a>Argumentos em funções de catálogo
Todas as funções de catálogo aceitam argumentos com que um aplicativo pode restringir o escopo dos dados retornados. Por exemplo, as primeira e segunda chamadas para **SQLTables** no código a seguir retorna um conjunto de resultados contendo informações sobre todas as tabelas, enquanto a terceira chamada retorna informações sobre a tabela Orders:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Argumentos de cadeia de caracteres da função de catálogo se enquadram em quatro tipos diferentes: argumento comum (OA), argumento de valor padrão (VP), argumento de identificador (ID) e o argumento de lista de valor (programa). A maioria dos argumentos de cadeia de caracteres pode ser de um dos dois tipos diferentes, dependendo do valor do atributo de instrução SQL_ATTR_METADATA_ID. A tabela a seguir lista os argumentos para cada função de catálogo e descreve o tipo do argumento de um valor SQL_TRUE ou SQL_FALSE SQL_ATTR_METADATA_ID.  
  
|Função|Argumento|Digite quando SQL _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Digite quando SQL _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID DE ID DE ID DE ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID DE ID DE ID DE ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName*  *FKTableName*|OA OA OA OA OA OA|ID ID ID ID IDENTIFICAÇÃO ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID DA ID DE ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID DE ID DE ID DE ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID DA ID DE ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID DA ID DE ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID DA ID DE ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID DA ID DE ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|VP PV PV PROGRAMA|PROGRAMA DE ID DE ID DE ID|  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Argumentos comuns](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argumentos do identificador](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumentos da lista de valor](../../../odbc/reference/develop-app/value-list-arguments.md)
