---
description: SQLSetStmtOption (Drivers de banco de dados de área de trabalho)
title: SQLSetStmtOption (drivers de banco de dados de desktop) | Microsoft Docs
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
ms.openlocfilehash: 0696ee98dd88f1c23120ef1d96c6e8d93751f76e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449148"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (Drivers de banco de dados de área de trabalho)

|*fOption*|Comentários|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|Não há suporte para o processamento assíncrono. O SQL_ASYNC_ENABLE fOption retornará SQLSTATE S1C00 (driver não compatível).|  
|SQL_KEYSET_SIZE|O único tamanho de conjunto de chaves válido é 0, pois não há suporte para cursores mistos e dinâmicos. Se esse valor for definido como qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_MAX_ROWS|O único tamanho válido do conjunto de linhas é 0, pois os drivers do banco de dados da área de trabalho não dão suporte à limitação do número de linhas retornadas. Se esse valor for definido como qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_QUERY_TIMEOUT|Não há suporte.|  
|SQL_ROW_NUMBER|Não há suporte.|  
|SQL_SIMULATE_CURSOR|Não há suporte.|
