---
title: "Funções em ODBC de catálogo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74b86dfd62a12938d18b4aa11a8d0502db50da13
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-functions-in-odbc"></a>Funções de catálogo em ODBC
ODBC contém as seguintes funções de catálogo:  
  
|Função|Description|  
|--------------|-----------------|  
|**SQLTables**|Retorna uma lista de catálogos, esquemas, tabelas ou tipos de tabela na fonte de dados.|  
|**SQLColumns**|Retorna uma lista de colunas em uma ou mais tabelas.|  
|**SQLStatistics**|Retorna uma lista de estatísticas sobre uma única tabela. Também retorna uma lista de índices associados à tabela.|  
|**SQLSpecialColumns**|Retorna uma lista de colunas que identifica exclusivamente uma linha em uma única tabela. Também retorna uma lista de colunas na tabela que são atualizadas automaticamente.|  
|**SQLPrimaryKeys**|Retorna uma lista de colunas que compõem a chave primária de uma única tabela.|  
|**SQLForeignKeys**|Retorna uma lista de chaves estrangeiras em uma única tabela ou uma lista de chaves estrangeiras em outras tabelas que fazem referência a uma única tabela.|  
|**SQLTablePrivileges**|Retorna uma lista de privilégios associados a uma ou mais tabelas.|  
|**SQLColumnPrivileges**|Retorna uma lista de privilégios associados a uma ou mais colunas em uma única tabela.|  
|**SQLProcedures**|Retorna uma lista de procedimentos na fonte de dados.|  
|**SQLProcedureColumns**|Retorna uma lista de parâmetros de entrada e saída, o valor de retorno e as colunas no conjunto de resultados de um único procedimento.|  
|**SQLGetTypeInfo**|Retorna uma lista dos tipos de dados SQL suportado pela fonte de dados. Esses tipos de dados são geralmente usados em **CREATE TABLE** e **ALTER TABLE** instruções.|  
  
 Porque **SQLTables**, **SQLColumns**, **SQLStatistics**, e **SQLSpecialColumns** em conformidade com a CLI do grupo aberto e **SQLGetTypeInfo** está em conformidade com ISO CLI 92, eles são implementados pela maioria dos drivers. As funções de catálogo restantes são em nível de conformidade do ODBC.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Exibições do esquema](../../../odbc/reference/develop-app/schema-views.md)
