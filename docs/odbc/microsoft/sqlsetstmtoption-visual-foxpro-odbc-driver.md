---
title: SQLSetStmtOption (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9d7bcecfbd880f53d1067fd68202b62c34fce398
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305817"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível 1  
  
 Define opções relacionadas a um identificador de instrução *hstmt*.  
  
|*fOption*|Valores permitidos|Comentários|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Se você tentar definir isso *fOption*, o driver retorna o erro: "O driver não funciona". Do Visual FoxPro não oferece suporte a execução assíncrona.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN ou um valor de 32 bits que indica o comprimento da estrutura ou uma instância de um buffer em qual resultado colunas serão associadas.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|O driver não permite SQL_CONCUR_ROWVER, porque o Visual FoxPro não tem controle de versão de linha com base em carimbos de hora.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|O driver não permite SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC; ver [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obter mais informações.|  
|SQL_KEYSET_SIZE|Erro: "Não têm a capacidade de driver"|Do Visual FoxPro não oferece suporte para o modelo de cursor de conjunto de chaves.|  
|SQL_MAX_LENGTH|0|Se você tentar definir isso *fOption* valor, o driver retorna o erro "Não têm a capacidade de Driver".|  
|SQL_MAX_ROWS|0|Se você tentar definir isso *fOption* valor, o driver retorna o erro "Não têm a capacidade de Driver".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Se você tentar definir isso *fOption* valor, o driver retorna o erro "Não têm a capacidade de Driver".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 para 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Erro: "Não têm a capacidade de driver"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obter mais informações, consulte [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) na *referência do programador de ODBC*.
