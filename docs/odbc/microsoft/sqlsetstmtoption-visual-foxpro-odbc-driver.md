---
title: SQLSetStmtOption (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77cd6f6f8ddd09a011dba2cbbe39c962d78b4574
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade de API de ODBC: Nível 1  
  
 Define opções relacionadas a um identificador de instrução, *hstmt*.  
  
|*fOption*|Valores permitidos|Comentários|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Se você tentar definir isso *fOption*, o driver retornará o erro: "O Driver não funciona". Do Visual FoxPro não oferece suporte à execução assíncrona.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN ou um valor de 32 bits que indica o comprimento da estrutura ou uma instância de um buffer em qual resultado colunas serão associadas.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|O driver não permite SQL_CONCUR_ROWVER, porque Visual FoxPro não têm controle de versão de linha com base em carimbos de hora.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|O driver não permite SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC; consulte [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obter mais informações.|  
|SQL_KEYSET_SIZE|Erro: "o Driver não funciona"|Do Visual FoxPro não oferece suporte para o modelo de cursor de conjunto de chaves.|  
|SQL_MAX_LENGTH|0|Se você tentar definir isso *fOption* valor, o driver retorna o erro "Não compatível com Driver".|  
|SQL_MAX_ROWS|0|Se você tentar definir isso *fOption* valor, o driver retorna o erro "Não compatível com Driver".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Se você tentar definir isso *fOption* valor, o driver retorna o erro "Não compatível com Driver".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 para 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Erro: "o Driver não funciona"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obter mais informações, consulte [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) no *referência do programador de ODBC*.
