---
title: Chamadas de função escalar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24b62c2b5cd449b6e7201d413b315e48fbd570f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468793"
---
# <a name="scalar-function-calls"></a>Chamadas de função escalar
Funções escalares retornam um valor para cada linha. Por exemplo, a função escalar do valor absoluto considera uma coluna numérica como um argumento e retorna o valor absoluto de cada valor na coluna. É a sequência de escape para chamar uma função escalar  
  
 **{fn** _função escalar_ **}**  
  
 em que *função escalar* é uma das funções listadas no [apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obter mais informações sobre a sequência de escape de função escalar, consulte [sequência de Escape de função escalar](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) no Apêndice c: Gramática SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados de cliente em maiusculas nomes. A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe de nativa para Ingres para o sistema operacional/2 e não é interoperável.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Um aplicativo pode misturar chamadas para funções escalares que usam sintaxe nativo e chamadas para funções escalares que usam a sintaxe ODBC. Por exemplo, suponha que os nomes na tabela de funcionários são armazenados como um nome, uma vírgula e um sobrenome. A instrução SQL a seguir cria um conjunto de resultados de sobrenomes de funcionários na tabela de funcionários. A instrução usa a função escalar de ODBC **subcadeia de caracteres** e a função escalar do SQL Server **CHARINDEX** e será executado corretamente apenas no SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Para interoperabilidade máxima, os aplicativos devem usar o **converter** função escalar para certificar-se de que a saída de uma função escalar é o tipo solicitado. O **converter** função converte dados de um tipo de dados SQL para o tipo de dados SQL especificado. A sintaxe do **converter** é de função  
  
 **CONVERT(** _value_exp_ **,** _data_type_ **)**  
  
 em que *value_exp* é um nome de coluna, o resultado de outra função escalar ou um valor literal, e *data_type* é uma palavra-chave que corresponda a **#define** nome que é usado por um Identificador de tipo de dados SQL conforme definido em [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md). Por exemplo, a seguinte instrução SQL usa o **converter** função para ter certeza de que a saída da **CURDATE** função for uma data, em vez de um caractere ou carimbo de hora de dados:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar quais funções escalares são suportadas por uma fonte de dados, um aplicativo chama **SQLGetInfo** com SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS e SQL_TIMEDATE_ Opções de funções. Para determinar quais operações de conversão têm suporte a **converter** função, um aplicativo chama **SQLGetInfo** com qualquer uma das opções que começam com SQL_CONVERT.
