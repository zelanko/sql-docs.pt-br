---
description: Funções de catálogo em ODBC
title: Funções de catálogo no ODBC | Microsoft Docs
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
ms.openlocfilehash: b7a34a29e55f6705ccc98e5644096ac6ea7bfd67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465968"
---
# <a name="catalog-functions-in-odbc"></a>Funções de catálogo em ODBC
O ODBC contém as seguintes funções de catálogo:  
  
|Função|Descrição|  
|--------------|-----------------|  
|**SQLTables**|Retorna uma lista de catálogos, esquemas, tabelas ou tipos de tabela na fonte de dados.|  
|**SQLColumns**|Retorna uma lista de colunas em uma ou mais tabelas.|  
|**SQLStatistics**|Retorna uma lista de estatísticas sobre uma única tabela. Também retorna uma lista de índices associados a essa tabela.|  
|**SQLSpecialColumns**|Retorna uma lista de colunas que identifica exclusivamente uma linha em uma única tabela. Também retorna uma lista de colunas nessa tabela que são atualizadas automaticamente.|  
|**SQLPrimaryKeys**|Retorna uma lista de colunas que compõem a chave primária de uma única tabela.|  
|**SQLForeignKeys**|Retorna uma lista de chaves estrangeiras em uma única tabela ou uma lista de chaves estrangeiras em outras tabelas que se referem a uma única tabela.|  
|**SQLTablePrivileges**|Retorna uma lista de privilégios associados a uma ou mais tabelas.|  
|**SQLColumnPrivileges**|Retorna uma lista de privilégios associados a uma ou mais colunas em uma única tabela.|  
|**SQLProcedures**|Retorna uma lista de procedimentos na fonte de dados.|  
|**SQLProcedureColumns**|Retorna uma lista de parâmetros de entrada e saída, o valor de retorno e as colunas no conjunto de resultados de um único procedimento.|  
|**SQLGetTypeInfo**|Retorna uma lista dos tipos de dados SQL com suporte pela fonte de dados. Esses tipos de dados geralmente são usados em instruções **CREATE TABLE** e **ALTER TABLE** .|  
  
 Como o **SQLTables**, o **SQLColumns**, o **SQLStatistics**e o **SQLSpecialColumns** estão em conformidade com a CLI do grupo aberto e o **SQLGetTypeInfo** está de acordo com a CLI do ISO 92, eles são implementados pela maioria dos drivers. As funções de catálogo restantes estão no nível de compatibilidade ODBC.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Exibições de esquema](../../../odbc/reference/develop-app/schema-views.md)
