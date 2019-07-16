---
title: Conformidade de atributo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71f0da7bbd7ef1a37a1f48539c7230bff0ceda15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909910"
---
# <a name="attribute-conformance"></a>Conformidade de atributo
A tabela a seguir indica o nível de conformidade de cada atributo de ambiente ODBC, que isso é bem definido.  
  
|Função|nível de conformidade|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|Core|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] este é um recurso opcional e como tal, não faz parte dos níveis de conformidade.  
  
 A tabela a seguir indica o nível de conformidade de cada atributo de conexão ODBC, que isso é bem definido.  
  
|Função|nível de conformidade|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|Core|  
|SQL_ATTR_ASYNC_ENABLE|Nível 1 ou nível 2 [1]|  
|SQL_ATTR_AUTO_IPD|Nível 2|  
|SQL_ATTR_AUTOCOMMIT|Nível 1|  
|SQL_ATTR_CONNECTION_DEAD|Nível 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|Nível 2|  
|SQL_ATTR_CURRENT_CATALOG|Nível 2|  
|SQL_ATTR_LOGIN_TIMEOUT|Nível 2|  
|SQL_ATTR_ODBC_CURSORS|Core|  
|SQL_ATTR_PACKET_SIZE|Nível 2|  
|SQL_ATTR_QUIET_MODE|Core|  
|SQL_ATTR_TRACE|Core|  
|SQL_ATTR_TRACEFILE|Core|  
|SQL_ATTR_TRANSLATE_LIB|Core|  
|SQL_ATTR_TRANSLATE_OPTION|Core|  
|SQL_ATTR_TXN_ISOLATION|Nível 1 ou nível 2 [2]|  
  
 [1] os aplicativos que dão suporte à assincronia do nível de conexão (necessária para o nível 1) devem dar suporte a configuração deste atributo como SQL_TRUE chamando **SQLSetConnectAttr**; o atributo não precisa ser configurável para um valor diferente de seu padrão valor por meio **SQLSetStmtAttr**. Aplicativos que dão suporte à assincronia de nível de instrução (necessária para o nível 2) devem dar suporte a configuração deste atributo como SQL_TRUE usando qualquer função.  
  
 [2] para conformidade de interface de nível 1, o driver deve oferecer suporte a um valor além do valor padrão definido pelo driver (disponíveis por meio da chamada **SQLGetInfo** com a opção SQL_DEFAULT_TXN_ISOLATION). Para conformidade de interface de nível 2, o driver também deve suportar SQL_TXN_SERIALIZABLE.  
  
 A tabela a seguir indica o nível de conformidade de cada atributo de instrução ODBC, que isso é bem definido.  
  
|Função|nível de conformidade|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|Core|  
|SQL_ATTR_APP_ROW_DESC|Core|  
|SQL_ATTR_ASYNC_ENABLE|Nível 1 ou nível 2 [1]|  
|SQL_ATTR_CONCURRENCY|Nível 1 ou nível 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|Nível 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|Nível 2|  
|SQL_ATTR_CURSOR_TYPE|Nível/Core 2 [3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|Nível 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Nível 2|  
|SQL_ATTR_IMP_PARAM_DESC|Core|  
|SQL_ATTR_IMP_ROW_DESC|Core|  
|SQL_ATTR_KEYSET_SIZE|Nível 2|  
|SQL_ATTR_MAX_LENGTH|Nível 1|  
|SQL_ATTR_MAX_ROWS|Nível 1|  
|SQL_ATTR_METADATA_ID|Core|  
|SQL_ATTR_NOSCAN|Core|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_PARAM_BIND_TYPE|Core|  
|SQL_ATTR_PARAM_OPERATION_PTR|Core|  
|SQL_ATTR_PARAM_STATUS_PTR|Core|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|Core|  
|SQL_ATTR_PARAMSET_SIZE|Core|  
|SQL_ATTR_QUERY_TIMEOUT|Nível 2|  
|SQL_ATTR_RETRIEVE_DATA|Nível 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|Core|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_ROW_BIND_TYPE|Core|  
|SQL_ATTR_ROW_NUMBER|Nível 1|  
|SQL_ATTR_ROW_OPERATION_PTR|Nível 1|  
|SQL_ATTR_ROW_STATUS_PTR|Core|  
|SQL_ATTR_ROWS_FETCHED_PTR|Core|  
|SQL_ATTR_SIMULATE_CURSOR|Nível 2|  
|SQL_ATTR_USE_BOOKMARKS|Nível 2|  
  
 [1] os aplicativos que dão suporte à assincronia do nível de conexão (necessária para o nível 1) devem dar suporte a configuração deste atributo como SQL_TRUE chamando **SQLSetConnectAttr**; o atributo não precisa ser configurável para um valor diferente de seu padrão valor por meio **SQLSetStmtAttr**. Aplicativos que dão suporte à assincronia de nível de instrução (necessária para o nível 2) devem dar suporte a configuração deste atributo como SQL_TRUE usando qualquer função.  
  
 [2] para conformidade de interface de nível 2, o driver deve oferecer suporte a SQL_CONCUR_READ_ONLY e pelo menos um outro valor.  
  
 [3] para conformidade de interface de nível 1, o driver deve oferecer suporte a SQL_CURSOR_FORWARD_ONLY e pelo menos um outro valor. Para conformidade de interface de nível 2, o driver deve oferecer suporte a todos os valores definidos neste documento.
