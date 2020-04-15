---
title: Argumentos em Funções de Catálogo | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288162"
---
# <a name="arguments-in-catalog-functions"></a>Argumentos em funções de catálogo
Todas as funções do catálogo aceitam argumentos com os quais um aplicativo pode restringir o escopo dos dados retornados. Por exemplo, a primeira e segunda chamadas para **SQLTables** no seguinte código retornam um conjunto de resultados contendo informações sobre todas as tabelas, enquanto a terceira chamada retorna informações sobre a tabela Ordens:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Os argumentos de seqüência de funções de catálogo se enquadram em quatro tipos diferentes: argumento ordinário (OA), argumento de valor padrão (PV), argumento de identificador (ID) e argumento de lista de valor (VL). A maioria dos argumentos de string pode ser de um dos dois tipos diferentes, dependendo do valor do atributo de declaração SQL_ATTR_METADATA_ID. A tabela a seguir lista os argumentos de cada função de catálogo e descreve o tipo do argumento para um valor SQL_TRUE ou SQL_FALSE de SQL_ATTR_METADATA_ID.  
  
|Função|Argumento|Digite quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Digite quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatálogoNome* *EsquemanomeNome* *TabelaNome* *ColumnName*|OA OA OA PV|ID ID ID ID|  
|**SQLColumns**|*CatálogoNome* *EsquemanomeNome* *TabelaNome* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID ID ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID ID ID|  
|**SQLTables**|*CatálogoNome* *EsquemanomeTabelaNome* *TableName* *TabelaType*|PV PV PV VL|ID ID ID VL|  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Argumentos comuns](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argumentos do identificador](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumentos da lista de valor](../../../odbc/reference/develop-app/value-list-arguments.md)
