---
description: SQLSetConnectOption (Driver do Excel)
title: SQLSetConnectOption (driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Excel Driver
- Excel driver [ODBC], SQLSetConnectOption
ms.assetid: 528d21d1-4516-4497-9da4-7b87d77e622a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c1d3294c090537dd68d5194da8bdc6cbfbcb4e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411752"
---
# <a name="sqlsetconnectoption-excel-driver"></a>SQLSetConnectOption (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|O SQL_ACCESS_MODE fOption pode ser definido como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impedirá atualizações se SQL_ACCESS_MODE estiver definido como SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|O driver do Microsoft Excel dá suporte apenas a SQL_AUTOCOMMIT sendo definido como ON (o estado padrão), porque eles não dão suporte a transações.|  
|SQL_CURRENT_QUALIFIER|Com suporte.|  
|SQL_LOGIN_TIMEOUT|Não há suporte.|  
|SQL_OPT_TRACE|Com suporte.|  
|SQL_OPT_TRACEFILE|Com suporte.|  
|SQL_PACKET_SIZE|Não há suporte.|  
|SQL_QUIET_MODE|Não há suporte.|  
|SQL_TRANSLATE_DLL|Não há suporte.|  
|SQL_TRANSLATION_OPTION|Não há suporte.|  
|SQL_TXN_ISOLATION|Não há suporte.|
