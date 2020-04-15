---
title: Exemplos de conversão de dados C para SQL | Microsoft Docs
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
ms.openlocfilehash: 0e21654f183946675c63cee10a3c08754e1508f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291986"
---
# <a name="c-to-sql-data-conversion-examples"></a>Exemplos de conversão de dados de C para SQL
Os exemplos a seguir ilustram como o driver converte dados C em dados SQL:  
  
|Identificador de tipo C|Valor dos dados C|Tipo SQL<br /><br /> identificador|Coluna<br /><br /> comprimento|Dados SQL<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|6|abcdef|n/d|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|5|Abcde|22001|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|8[b]|1234.56|n/d|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|7[b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/d|1234.56|n/d|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/d|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/d|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|10|1992-12-31|n/d|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_TIMESTAMP|n/d|1992-12-31 00:00:00.0|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 1200000000[d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 1200000000[d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 1200000000[d]|SQL_CHAR|18|----|22003|  
  
 [a] "\0" representa um byte de rescisão nula. O byte de rescisão nula só é exigido se o comprimento dos dados for SQL_NTS.  
  
 [b] Além dos bytes para números, um byte é necessário para um sinal e outro byte é necessário para o ponto decimal.  
  
 [c] Os números desta lista são os números armazenados nos campos da estrutura SQL_DATE_STRUCT.  
  
 [d] Os números desta lista são os números armazenados nos campos da estrutura SQL_TIMESTAMP_STRUCT.
