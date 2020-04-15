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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349599a51b2996f419e6c8656a71bc9e30146542
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304257"
---
# <a name="scalar-function-calls"></a>Chamadas de função escalar
As funções escalares retornam um valor para cada linha. Por exemplo, a função escalar de valor absoluto toma uma coluna numérica como argumento e retorna o valor absoluto de cada valor na coluna. A seqüência de fuga para chamar uma função escalar é  
  
 **{fn**  _escalador-function_ **}**  
  
 onde *a função escalar* é uma das funções listadas no [apêndice E: Funções Escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obter mais informações sobre a seqüência de fuga da função escalar, consulte [Seqüência](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) de fuga de função escalar no apêndice C: Gramática SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados de nomes de clientes em maiúsculas. A primeira declaração usa a sintaxe de seqüência de fuga. A segunda declaração usa a sintaxe nativa para Ingres para OS/2 e não é interoperável.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Um aplicativo pode misturar chamadas para funções escalares que usam sintaxe nativa e chamadas para funções escalares que usam sintaxe ODBC. Por exemplo, suponha que os nomes na tabela Funcionário sejam armazenados como sobrenome, uma comuma e um primeiro nome. A seguinte declaração SQL cria um conjunto de resultados de sobrenomes de funcionários na tabela Funcionários. A declaração usa a função escalar ODBC **SUBSTRING** e a função escalar sql server **CHARINDEX** e será executada corretamente apenas no SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Para interoperabilidade máxima, as aplicações devem usar a função **ESCALAR CONVERT** para certificar-se de que a saída de uma função escalar é o tipo necessário. A função **CONVERT** converte dados de um tipo de dados SQL para o tipo de dados SQL especificado. A sintaxe da função **CONVERT** é  
  
 **CONVERT(** _(value_exp,_ **,** _data_type)_**)**  
  
 onde *value_exp* é um nome de coluna, o resultado de outra função escalar, ou um valor literal, e *data_type* é uma palavra-chave que corresponde ao nome **#define** que é usado por um identificador de tipo de dados SQL como definido no [apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md). Por exemplo, a seguinte declaração SQL usa a função **CONVERT** para certificar-se de que a saída da função **CURDATE** é uma data, em vez de um carimbo de tempo ou dados de caracteres:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar quais funções escalares são suportadas por uma fonte de dados, um aplicativo chama **sqlGetInfo** com as opções SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS e SQL_TIMEDATE_FUNCTIONS. Para determinar quais operações de conversão são suportadas pela função **CONVERT,** um aplicativo chama **SQLGetInfo** com qualquer uma das opções que começam com SQL_CONVERT.
