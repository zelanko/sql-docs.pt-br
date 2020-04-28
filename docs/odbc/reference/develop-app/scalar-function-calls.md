---
title: Chamadas de função escalares | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304257"
---
# <a name="scalar-function-calls"></a>Chamadas de função escalar
As funções escalares retornam um valor para cada linha. Por exemplo, a função escalar de valor absoluto usa uma coluna numérica como um argumento e retorna o valor absoluto de cada valor na coluna. A sequência de escape para chamar uma função escalar é  
  
 **{FN**  _-função escalar_ **}**  
  
 onde *escalar-function* é uma das funções listadas no [Apêndice E: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obter mais informações sobre a sequência de escape de função escalar, consulte [sequência de escape de função escalar](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) no Apêndice C: gramática SQL.  
  
 Por exemplo, as instruções SQL a seguir criam o mesmo conjunto de resultados de nomes de clientes em maiúsculas. A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe nativa para entrada para o sistema operacional/2 e não é interoperável.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Um aplicativo pode misturar chamadas para funções escalares que usam sintaxe nativa e chamadas para funções escalares que usam sintaxe ODBC. Por exemplo, suponha que os nomes na tabela Employee sejam armazenados como um sobrenome, uma vírgula e um nome. A instrução SQL a seguir cria um conjunto de resultados dos últimos nomes de funcionários na tabela Employee. A instrução usa a **subcadeia de caracteres** da função escalar do ODBC e a função SQL Server escalar **charIndex** e será executada corretamente somente em SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Para obter a interoperabilidade máxima, os aplicativos devem usar a função **Convert** escalar para garantir que a saída de uma função escalar seja o tipo necessário. A função **Convert** converte dados de um tipo de dados SQL para o tipo de dados SQL especificado. A sintaxe da função **Convert** é  
  
 **Convert (** _value_exp_ **,** _data_type_**)**  
  
 em que *value_exp* é um nome de coluna, o resultado de outra função escalar, ou um valor literal, e *data_type* é uma palavra-chave que corresponde ao nome de **#define** usado por um identificador de tipo de dados SQL, conforme definido no [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md). Por exemplo, a instrução SQL a seguir usa a função **Convert** para certificar-se de que a saída da função **CURDATE** é uma data, em vez de um timestamp ou dados de caractere:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar quais funções escalares são suportadas por uma fonte de dados, um aplicativo chama **SQLGetInfo** com as opções SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS e SQL_TIMEDATE_FUNCTIONS. Para determinar quais operações de conversão são suportadas pela função **Convert** , um aplicativo chama **SQLGetInfo** com qualquer uma das opções que começam com SQL_CONVERT.
