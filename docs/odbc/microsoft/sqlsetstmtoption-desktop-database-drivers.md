---
title: SQLSetStmtOption (Drivers de banco de dados da área de trabalho) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48dc5dff83e942b894548d44e3673c19ca0746c5
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044869"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (Drivers de banco de dados de área de trabalho)

|*fOption*|Comentários|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|Não há suporte para o processamento assíncrono. O fOption SQL_ASYNC_ENABLE retornará SQLSTATE S1C00 (o Driver não funciona).|  
|SQL_KEYSET_SIZE|O tamanho do conjunto de chaves só é válida é 0, porque misto e não há suporte para cursores dinâmicos. Se esse valor é definido como qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor de opção alterado).|  
|SQL_MAX_ROWS|O tamanho do conjunto de linhas somente válido é 0, pois os Drivers de banco de dados de área de trabalho não suportam limitando o número de linhas retornadas. Se esse valor é definido como qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor de opção alterado).|  
|SQL_QUERY_TIMEOUT|Sem suporte.|  
|SQL_ROW_NUMBER|Sem suporte.|  
|SQL_SIMULATE_CURSOR|Sem suporte.|
