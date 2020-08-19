---
description: Exemplos de conversão de dados de SQL para C
title: Exemplos de conversão de dados de SQL para C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a7a3d70a6f74a814262ddad580b5e5a2b0d79927
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429578"
---
# <a name="sql-to-c-data-conversion-examples"></a>Exemplos de conversão de dados de SQL para C

Os exemplos mostrados na tabela a seguir ilustram como o driver converte dados SQL em dados C:  
  
|Tipo SQL<br /><br /> identificador|Dados SQL<br /><br /> value|Tipo de C<br /><br /> identificador|Buffer<br /><br /> comprimento|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|n/d|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234,56|SQL_C_CHAR|8|1234.56 \ 0 [a]|n/d|  
|SQL_DECIMAL|1234,56|SQL_C_CHAR|5|1234 \ 0 [a]|01004|  
|SQL_DECIMAL|1234,56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234,56|SQL_C_FLOAT|ignorado|1234,56|n/d|  
|SQL_DECIMAL|1234,56|SQL_C_SSHORT|ignorado|1234|01S07|  
|SQL_DECIMAL|1234,56|SQL_C_STINYINT|ignorado|----|22003|  
|SQL_DOUBLE|1,2345678|SQL_C_DOUBLE|ignorado|1,2345678|n/d|  
|SQL_DOUBLE|1,2345678|SQL_C_FLOAT|ignorado|1,234567|n/d|  
|SQL_DOUBLE|1,2345678|SQL_C_STINYINT|ignorado|1|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31 \ 0 [a]|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|ignorado|1992, 12, 31, 0, 0, 0, 0 [b]|n/d|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|1992-12-31 23:45:55.12 \ 0 [a]|n/d|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|1992-12-31 23:45:55.1 \ 0 [a]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\ 0" representa um byte de terminação nula. O driver sempre nulo – encerra SQL_C_CHAR dados.  
  
 [b] os números nessa lista são os números armazenados nos campos da estrutura de TIMESTAMP_STRUCT.
