---
title: Arquivos de cabeçalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d31cdda9e97ba72374c60c551f37ecfeccd71c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912391"
---
# <a name="header-files"></a>Arquivos de cabeçalho
O arquivo de cabeçalho do SQL contém protótipos para as funções e recursos no nível de conformidade a principal Interface de ODBC. O arquivo de cabeçalho Sqlext.h contém protótipos para as funções e recursos no nível 1 e níveis de conformidade de API do nível 2. O arquivo de cabeçalho sqlext contém definições de tipo e indicadores para os tipos de dados SQL.  
  
 Os arquivos de cabeçalho contêm um **#define**, ODBCVER, que pode ser definidas por um aplicativo ou driver a ser compilado para diferentes versões do ODBC.  
  
 Para alinhar com o ISO CLI e abra CLI de grupo, os arquivos de cabeçalho contêm aliases para os tipos de informações usados em chamadas para **SQLGetInfo**. Na tabela a seguir, a coluna "Nome do ODBC" indica o nome do ODBC para o tipo de informações em [referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md). A coluna "Alias no arquivo de cabeçalho" indica o nome que é usado em CLI ISO e a CLI do grupo aberto. O valor numérico real desses nomes de manifesto é o mesmo no ODBC e as CLIs padrão. Esses aliases permitem que um aplicativo compatível com os padrões ou o driver compilar com o ODBC 3 *. x* arquivos de cabeçalho.  
  
 Esses aliases incluem expansões de abreviações em nomes de ODBC para que os nomes sejam mais compreensíveis. "MAX" é expandido para "Máximo", "LEN" para "Comprimento", "MULT" para "Várias", "OJ" para "OUTER_JOIN" e "TXN" para "Transação".  
  
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
