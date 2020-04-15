---
title: SQLSetConnectOption (driver de acesso) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e5f15575d34031d9886219af5677b4fc5f1d5aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301529"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do Access Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOpção|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|A opção SQL_ACCESS_MODE f pode ser definida como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impede atualizações se SQL_ACCESS_MODE estiver definido para SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Quando o driver microsoft access é usado, a opção SQL_AUTOCOMMIT pode ser definida como SQL_AUTOCOMMIT_ON ou SQL_AUTOCOMMIT_OFF, porque o driver do Microsoft Access suporta transações[1].|  
|SQL_CURRENT_QUALIFIER| Com suporte.|  
|SQL_LOGIN_TIMEOUT|Sem suporte.|  
|SQL_OPT_TRACE| Com suporte.|  
|SQL_OPT_TRACEFILE| Com suporte.|  
|SQL_PACKET_SIZE|Sem suporte.|  
|SQL_QUIET_MODE|Sem suporte.|  
|SQL_TRANSLATE_DLL|Sem suporte.|  
|SQL_TRANSLATION_OPTION|Sem suporte.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION está sempre SQL_TXN_READ_COMMITTED.|  
  
 [1] As transações atômicas não são suportadas pelo driver microsoft access. Ao cometer uma transação usando o driver Microsoft Access, existe um atraso finito entre o momento em que a transação é comprometida e o momento em que os valores são gravados em disco. Esse atraso é determinado por um atraso inerente ao motor Microsoft Jet. O tempo limite da página não será inferior a um valor mínimo, mesmo que a opção PageTimeout esteja definida abaixo desse valor. Como resultado, não há garantia de que os dados comprometidos sejam estáveis, uma vez que alterações podem ser feitas durante o atraso.
