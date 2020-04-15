---
title: Funções do Catálogo na ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6731018b99f2f3043e48ee7c174a08cb9ef71fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306227"
---
# <a name="catalog-functions-in-odbc"></a>Funções de catálogo em ODBC
O DBC contém as seguintes funções de catálogo:  
  
|Função|Descrição|  
|--------------|-----------------|  
|**SQLTables**|Retorna uma lista de catálogos, esquemas, tabelas ou tipos de tabela na fonte de dados.|  
|**SQLColumns**|Retorna uma lista de colunas em uma ou mais tabelas.|  
|**SQLStatistics**|Retorna uma lista de estatísticas sobre uma única tabela. Também retorna uma lista de índices associados a essa tabela.|  
|**SQLSpecialColumns**|Retorna uma lista de colunas que identifica exclusivamente uma linha em uma única tabela. Também retorna uma lista de colunas nessa tabela que são atualizadas automaticamente.|  
|**SQLPrimaryKeys**|Retorna uma lista de colunas que compõem a chave principal de uma única tabela.|  
|**SQLForeignKeys**|Retorna uma lista de chaves estrangeiras em uma única tabela ou uma lista de chaves estrangeiras em outras tabelas que se referem a uma única tabela.|  
|**SQLTablePrivileges**|Retorna uma lista de privilégios associados a uma ou mais tabelas.|  
|**SQLColumnPrivileges**|Retorna uma lista de privilégios associados a uma ou mais colunas em uma única tabela.|  
|**SQLProcedures**|Retorna uma lista de procedimentos na fonte de dados.|  
|**SQLProcedureColumns**|Retorna uma lista de parâmetros de entrada e saída, o valor de retorno e as colunas no conjunto de resultados de um único procedimento.|  
|**SQLGetTypeInfo**|Retorna uma lista dos tipos de dados SQL suportados pela fonte de dados. Esses tipos de dados são geralmente usados em instruções **DE TABELA DE CRIAÇÃO** e TABELA DE **ALTER.**|  
  
 Como **sqltables,** **sqlcolumns,** **sqlstatistics**e **sqlspecialcolumns** estão em conformidade com o CLI do Grupo Aberto, e **o SQLGetTypeInfo** está em conformidade com a ISO 92 CLI, eles são implementados pela maioria dos drivers. As demais funções do catálogo estão no nível de conformidade ODBC.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Exibições do esquema](../../../odbc/reference/develop-app/schema-views.md)
