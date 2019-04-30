---
title: Função de conversão de tipo de dados explícita | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77cb69877324b36120b3a277688bb1ad737f5c4d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188980"
---
# <a name="explicit-data-type-conversion-function"></a>Função de conversão de tipo de dados explícitos
Conversão de tipo de dados explícito é especificada em termos de definições de tipo de dados SQL.  
  
 A sintaxe ODBC para a função de conversão de tipo de dados explícito não restringe conversões. A validade de conversões específicas de um tipo de dados para outro tipo de dados será determinada por cada implementação específica do driver. O driver, conforme ele converte a sintaxe ODBC para a sintaxe de nativa, rejeitará as conversões que, embora legal na sintaxe de ODBC, não têm suporte pela fonte de dados. A função ODBC **SQLGetInfo**, com a conversão opções (como SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH e assim por diante), fornece uma maneira para saber mais sobre as conversões com suporte pela fonte de dados .  
  
 O formato do **converter** função é:  
  
 **CONVERT(** _value_exp_, _data_type_**)**  
  
 A função retorna o valor especificado por *value_exp* convertido especificado *data_type*, onde *data_type* é uma das seguintes palavras-chave:  
  
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
  
 A sintaxe ODBC para a função de conversão de tipo de dados explícito não oferece suporte a especificação de formato de conversão. Se a especificação dos formatos explícitas tem suporte pela fonte de dados subjacente, um driver deve especificar um valor padrão ou implementar a especificação de formato.  
  
 O argumento *value_exp* pode ser um nome de coluna, o resultado de outra função escalar ou um numérico ou cadeia de caracteres literal. Por exemplo:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 Converte a saída da função escalar CURDATE em uma cadeia de caracteres.  
  
 Como o ODBC não exige um tipo de dados para valores de retorno de funções escalares (como as funções costumam ser específico de fonte de dados), aplicativos devem usar a função escalar CONVERT sempre que possível forçar a conversão de tipo de dados.  
  
 Os exemplos a seguir ilustram o uso do **converter** função. Estes exemplos supõem a existência de uma tabela chamada funcionários, com uma coluna do tipo SQL_SMALLINT de EMPNO e uma coluna de EMPNAME do tipo SQL_CHAR.  
  
 Se um aplicativo especifica a instrução SQL a seguir:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   Um driver para ORACLE converte a instrução SQL para:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   Um driver para SQL Server converte a instrução SQL para:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 Se um aplicativo especifica a instrução SQL a seguir:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   Um driver para ORACLE converte a instrução SQL para:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   Um driver para SQL Server converte a instrução SQL para:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Um driver para Ingres traduz a instrução SQL para:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
