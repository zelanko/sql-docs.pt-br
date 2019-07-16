---
title: SQLSetConnectOption (Driver do Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bea124a78e2a180180c59de3577fe1db7637e110
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897791"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Access. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|O fOption SQL_ACCESS_MODE pode ser definido como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impede que atualizações se SQL_ACCESS_MODE for definido como SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Quando o driver do Microsoft Access for usado, a opção SQL_AUTOCOMMIT pode ser definida como SQL_AUTOCOMMIT_ON ou SQL_AUTOCOMMIT_OFF, porque o driver do Microsoft Access dá suporte a transações [1].|  
|SQL_CURRENT_QUALIFIER|Com suporte.|  
|SQL_LOGIN_TIMEOUT|Sem suporte.|  
|SQL_OPT_TRACE|Com suporte.|  
|SQL_OPT_TRACEFILE|Com suporte.|  
|SQL_PACKET_SIZE|Sem suporte.|  
|SQL_QUIET_MODE|Sem suporte.|  
|SQL_TRANSLATE_DLL|Sem suporte.|  
|SQL_TRANSLATION_OPTION|Sem suporte.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION é sempre SQL_TXN_READ_COMMITTED.|  
  
 [1] não há suporte para transações atômicas no driver do Microsoft Access. Ao confirmar uma transação usando o driver do Microsoft Access, um atraso finito existe entre o momento em que a transação é confirmada e a hora em que os valores são gravados no disco. Esse atraso é determinado por um atraso inerente no mecanismo do Microsoft Jet. O tempo limite da página não pode ser menor que um valor mínimo, mesmo se a opção PageTimeout está definida abaixo desse valor. Como resultado, há nenhuma garantia de que foi confirmada dados é estável, pois as alterações podem ser feitas durante o atraso.
