---
title: SQLSetStmtOption (Drivers de banco de dados de desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69b386aee3f95fd047f72510dce7658130ac7aa5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299406"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (Drivers de banco de dados de área de trabalho)

|*fOpção*|Comentários|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|O processamento assíncrono não é suportado. O SQL_ASYNC_ENABLE fOption retornará SQLSTATE S1C00 (Driver não é capaz).|  
|SQL_KEYSET_SIZE|O único tamanho de chave de chave válido é 0, porque os cursores mistos e dinâmicos não são suportados. Se este valor for definido para qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_MAX_ROWS|O único tamanho de conjunto de linhas válido é 0, porque os drivers de banco de dados da área de trabalho não suportam limitar o número de linhas que são retornadas. Se este valor for definido para qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_QUERY_TIMEOUT|Sem suporte.|  
|SQL_ROW_NUMBER|Sem suporte.|  
|SQL_SIMULATE_CURSOR|Sem suporte.|
