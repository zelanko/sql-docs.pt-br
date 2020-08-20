---
description: Exemplos de conversão de dados de C para SQL
title: Exemplos de conversão de dados de C para SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65b0dd229139de060dd79132ee3ca7215906442a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500009"
---
# <a name="c-to-sql-data-conversion-examples"></a>Exemplos de conversão de dados de C para SQL
Os exemplos a seguir ilustram como o driver converte dados C em dados SQL:  
  
|Identificador de tipo C|Valor de dados C|Tipo SQL<br /><br /> identificador|Coluna<br /><br /> comprimento|Dados SQL<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|n/d|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|8 [b]|1234,56|n/d|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|7 [b]|1234,5|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234,56|SQL_FLOAT|n/d|1234,56|n/d|  
|SQL_C_FLOAT|1234,56|SQL_INTEGER|n/d|1234|22001|  
|SQL_C_FLOAT|1234,56|SQL_TINYINT|n/d|----|22003|  
|SQL_C_TYPE_DATE|1992, 12, 31 [c]|SQL_CHAR|10|1992-12-31|n/d|  
|SQL_C_TYPE_DATE|1992, 12, 31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992, 12, 31 [c]|SQL_TIMESTAMP|n/d|1992-12-31 00:00:00.0|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992, 12, 31, 23, 45, 55, 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992, 12, 31, 23, 45, 55, 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992, 12, 31, 23, 45, 55, 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\ 0" representa um byte de terminação nula. O byte de terminação nula será necessário somente se o comprimento dos dados for SQL_NTS.  
  
 [b] Além de bytes para números, é necessário um byte para um sinal e outro byte é necessário para o ponto decimal.  
  
 [c] os números nessa lista são os números armazenados nos campos da estrutura de SQL_DATE_STRUCT.  
  
 [d] os números nessa lista são os números armazenados nos campos da estrutura de SQL_TIMESTAMP_STRUCT.
