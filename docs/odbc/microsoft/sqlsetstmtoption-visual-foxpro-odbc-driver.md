---
title: SQLSetStmtOption (Driver Visual FoxPro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb9677a9ccf307be847089c657964d96904eb20b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299396"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 1  
  
 Define opções relacionadas a uma alça de *declaração, hstmt*.  
  
|*fOpção*|Valores permitidos|Comentários|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Se você tentar definir esta *fOption,* o motorista retorna o erro: "Driver não é capaz". Visual FoxPro não suporta execução assíncrona.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN ou um valor de 32 bits denotando o comprimento da estrutura ou uma instância de um buffer no qual as colunas de resultado serão vinculadas.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|O driver não permite SQL_CONCUR_ROWVER, porque o Visual FoxPro não tem versões de linha baseadas em carimbos de tempo.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|O motorista não permite SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC; consulte [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obter mais informações.|  
|SQL_KEYSET_SIZE|Erro: "Driver não é capaz"|Visual FoxPro não suporta o modelo de cursor keyset.|  
|SQL_MAX_LENGTH|0|Se você tentar definir esse valor *fOption,* o driver retorna o erro "Driver não é capaz".|  
|SQL_MAX_ROWS|0|Se você tentar definir esse valor *fOption,* o driver retorna o erro "Driver não é capaz".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Se você tentar definir esse valor *fOption,* o driver retorna o erro "Driver não é capaz".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Erro: "Driver não é capaz"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obter mais informações, consulte [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) na *referência do programador ODBC*.
