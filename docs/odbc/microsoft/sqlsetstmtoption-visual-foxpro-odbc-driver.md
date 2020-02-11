---
title: SQLSetStmtOption (driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a026922cb98fdb520c9eeab223c8b34a231a179e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905336"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Define opções relacionadas a um identificador de instrução, *HSTMT*.  
  
|*fOption*|Valores permitidos|Comentários|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Se você tentar definir esse *fOption*, o driver retornará o erro: "driver não compatível". O Visual FoxPro não oferece suporte à execução assíncrona.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN ou um valor de 32 bits indicando o comprimento da estrutura ou uma instância de um buffer no qual as colunas de resultado serão associadas.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|O driver não permite SQL_CONCUR_ROWVER, porque o Visual FoxPro não tem controle de versão de linha com base em carimbos de data/hora.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|O driver não permite SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC; consulte [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obter mais informações.|  
|SQL_KEYSET_SIZE|Erro: "driver não compatível"|O Visual FoxPro não dá suporte ao modelo de cursor do conjunto de chaves.|  
|SQL_MAX_LENGTH|0|Se você tentar definir esse valor de *fOption* , o driver retornará o erro "driver não compatível".|  
|SQL_MAX_ROWS|0|Se você tentar definir esse valor de *fOption* , o driver retornará o erro "driver não compatível".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Se você tentar definir esse valor de *fOption* , o driver retornará o erro "driver não compatível".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Erro: "driver não compatível"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obter mais informações, consulte [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) na *referência do programador de ODBC*.
