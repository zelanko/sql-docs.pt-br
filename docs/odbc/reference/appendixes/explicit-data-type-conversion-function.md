---
title: Função de conversão explícita do tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de8a8cb6177e9210e8d48c0ce097d13c9a276fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306987"
---
# <a name="explicit-data-type-conversion-function"></a>Função de conversão de tipo de dados explícitos
A conversão explícita do tipo de dados é especificada em termos de definições de tipo de dados SQL.  
  
 A sintaxe ODBC para a função de conversão de tipo de dados explícitos não restringe as conversões. A validade de conversões específicas de um tipo de dados para outro tipo de dados será determinada por cada implementação específica do driver. O driver, pois traduz a sintaxe ODBC na sintaxe nativa, rejeitará as conversões que, embora legais na sintaxe ODBC, não são suportadas pela fonte de dados. A função ODBC **SQLGetInfo**, com as opções de conversão (como SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH e assim por diante), fornece uma maneira de perguntar sobre conversões suportadas pela fonte de dados.  
  
 O formato da função **CONVERT** é:  
  
 **CONVERT (** _value_exp_, _data_type)_**)**  
  
 A função retorna o valor especificado por *value_exp* convertido para o *data_type*especificado, onde *data_type* é uma das seguintes palavras-chave:  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 A sintaxe ODBC para a função de conversão de tipo de dados explícito satisfaz a especificação do formato de conversão. Se a especificação de formatos explícitos for suportada pela fonte de dados subjacente, um driver deve especificar um valor padrão ou implementar a especificação do formato.  
  
 O argumento *value_exp* pode ser um nome de coluna, o resultado de outra função escalar, ou um numérico ou literal de seqüência. Por exemplo:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 converte a saída da função escalar CURDATE para uma seqüência de caracteres.  
  
 Como o ODBC não obriga um tipo de dados para valores de retorno de funções escalares (porque as funções são muitas vezes específicas da fonte de dados), os aplicativos devem usar a função ESCALAR CONVERT sempre que possível para forçar a conversão do tipo de dados.  
  
 Os dois exemplos a seguir ilustram o uso da função **CONVERT.** Esses exemplos assumem a existência de uma tabela chamada EMPLOYEES, com uma coluna EMPNO de SQL_SMALLINT tipo e uma coluna EMPNAME de tipo SQL_CHAR.  
  
 Se um aplicativo especificar a seguinte declaração SQL:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   Um driver para ORACLE traduz a declaração SQL para:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   Um driver para SQL Server traduz a declaração SQL para:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 Se um aplicativo especificar a seguinte declaração SQL:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   Um driver para ORACLE traduz a declaração SQL para:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   Um driver para SQL Server traduz a declaração SQL para:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Um driver para Ingres traduz a declaração SQL para:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
