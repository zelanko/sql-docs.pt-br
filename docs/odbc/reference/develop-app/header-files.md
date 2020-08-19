---
description: Arquivos de cabeçalho
title: Arquivos de cabeçalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec8eede80f88f10e0b1ca43696e75dddec121ffe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476648"
---
# <a name="header-files"></a>Arquivos de cabeçalho
O arquivo de cabeçalho SQL. h contém protótipos para as funções e recursos no nível de conformidade da interface ODBC principal. O arquivo de cabeçalho sqlext. h contém protótipos para as funções e recursos nos níveis de conformidade da API nível 1 e nível 2. O arquivo de cabeçalho SqlTypes. h contém definições de tipo e indicadores para os tipos de dados SQL.  
  
 Todos os arquivos de cabeçalho contêm um **#define**, ODBCVER, que um aplicativo ou driver pode definir para ser compilado para versões diferentes do ODBC.  
  
 Para se alinhar com a CLI ISO e com a CLI do grupo aberto, os arquivos de cabeçalho contêm aliases para os tipos de informações usados em chamadas para **SQLGetInfo**. Na tabela a seguir, a coluna "nome do ODBC" indica o nome do ODBC para o tipo de informação na [referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md). A coluna "alias no arquivo de cabeçalho" indica o nome que é usado na CLI ISO e na CLI do grupo aberto. O valor numérico real desses nomes de manifesto é o mesmo tanto no ODBC quanto nas CLIs padrão. Esses aliases permitem que um aplicativo ou driver em conformidade com os padrões compile com os arquivos de cabeçalho ODBC *3. x* .  
  
 Esses aliases incluem expansões de abreviações nos nomes ODBC para que os nomes sejam mais compreensíveis. "MAX" é expandido para "MAXIMUM", "LEN" para "LENGTH", "MULT" para "MULTIPLE", "OJ" to "OUTER_JOIN" e "TXN" para "TRANSACTION".  
  
|Nome do ODBC|Alias no arquivo de cabeçalho|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
