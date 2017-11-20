---
title: "SQLSetStmtOption (Drivers do banco de dados de área de trabalho) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8d1f51805413056a06c6cee769920e1ad878abe5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (Drivers do banco de dados de área de trabalho)
|*fOption*|Comentários|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|Não há suporte para o processamento assíncrono. O fOption SQL_ASYNC_ENABLE retornará SQLSTATE S1C00 (o Driver não funciona).|  
|SQL_KEYSET_SIZE|O tamanho do conjunto de chaves só é válida é 0, porque misto e não há suporte para cursores dinâmicos. Se esse valor é definido como qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_MAX_ROWS|O tamanho do conjunto de linhas somente válido é 0, porque os Drivers de banco de dados de área de trabalho não oferecem suporte para a limitação do número de linhas retornadas. Se esse valor é definido como qualquer outro número, ele será alterado para 0 e a chamada retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_QUERY_TIMEOUT|Sem suporte.|  
|SQL_ROW_NUMBER|Sem suporte.|  
|SQL_SIMULATE_CURSOR|Sem suporte.|

