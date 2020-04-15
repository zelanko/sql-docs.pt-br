---
title: SQLSetConnectOption (driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Text File Driver
- text file driver [ODBC], SQLSetConnectOption
ms.assetid: b631a20c-2f60-4102-a61d-93b8780a4620
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6442134086ea6fe15b393b87d6c80019a076be2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306131"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver de arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOpção|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|A opção SQL_ACCESS_MODE f pode ser definida como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impede atualizações se SQL_ACCESS_MODE estiver definido para SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|O driver Texto só suporta SQL_AUTOCOMMIT sendo definido como ON (o estado padrão), porque eles não suportam transações.|  
|SQL_CURRENT_QUALIFIER| Com suporte.|  
|SQL_LOGIN_TIMEOUT|Sem suporte.|  
|SQL_OPT_TRACE| Com suporte.|  
|SQL_OPT_TRACEFILE| Com suporte.|  
|SQL_PACKET_SIZE|Sem suporte.|  
|SQL_QUIET_MODE|Sem suporte.|  
|SQL_TRANSLATE_DLL|Sem suporte.|  
|SQL_TRANSLATION_OPTION|Sem suporte.|  
|SQL_TXN_ISOLATION|Sem suporte.|
