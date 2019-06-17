---
title: C para exemplos de conversão de dados SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40cd9973bfdce68b1ccbe63edd8c875519dbd22b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201583"
---
# <a name="c-to-sql-data-conversion-examples"></a>Exemplos de conversão de dados de C para SQL
Os exemplos a seguir ilustram como o driver converte os dados de C aos dados do SQL:  
  
|Identificador de tipo C|Valor de dados C|Tipo SQL<br /><br /> identificador|coluna<br /><br /> comprimento|Dados SQL<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|6|abcdef|n/d|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|8[b]|1234.56|n/d|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|7[b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/d|1234.56|n/d|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/d|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/d|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|10|1992-12-31|n/d|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_TIMESTAMP|n/d|1992-12-31 00:00:00.0|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|18|----|22003|  
  
 [a] "\0" representa um byte nulo de terminação. O byte nulo de terminação é necessário somente se o comprimento dos dados é SQL_NTS.  
  
 [b] em além com bytes para números, um byte é necessário para um sinal e outro byte é necessária para o ponto decimal.  
  
 [c] os números nesta lista são os números armazenados nos campos da estrutura SQL_DATE_STRUCT.  
  
 [d] os números nesta lista são os números armazenados nos campos da estrutura de SQL_TIMESTAMP_STRUCT.
