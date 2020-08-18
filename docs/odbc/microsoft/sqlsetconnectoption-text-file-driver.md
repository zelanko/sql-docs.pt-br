---
description: SQLSetConnectOption (Driver de Arquivo de texto)
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
ms.openlocfilehash: 2247c6692da4ad88a51a69107f5f104df95eb96f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411622"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|O SQL_ACCESS_MODE fOption pode ser definido como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impedirá atualizações se SQL_ACCESS_MODE estiver definido como SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|O driver de texto só dá suporte a SQL_AUTOCOMMIT ser definido como ON (o estado padrão), porque eles não dão suporte a transações.|  
|SQL_CURRENT_QUALIFIER|Com suporte.|  
|SQL_LOGIN_TIMEOUT|Não há suporte.|  
|SQL_OPT_TRACE|Com suporte.|  
|SQL_OPT_TRACEFILE|Com suporte.|  
|SQL_PACKET_SIZE|Não há suporte.|  
|SQL_QUIET_MODE|Não há suporte.|  
|SQL_TRANSLATE_DLL|Não há suporte.|  
|SQL_TRANSLATION_OPTION|Não há suporte.|  
|SQL_TXN_ISOLATION|Não há suporte.|
