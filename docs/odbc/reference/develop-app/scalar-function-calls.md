---
title: Chamadas de função escalar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e69cc7382c73aaedda31a902cc8ed8daff5cff8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="scalar-function-calls"></a>Chamadas de função escalar
Funções escalares retornam um valor para cada linha. Por exemplo, a função escalar do valor absoluto considera uma coluna numérica como um argumento e retorna o valor absoluto de cada valor na coluna. É a sequência de escape para chamar uma função escalar  
  
 **{fn***função escalar* **}**   
  
 onde *função escalar* é uma das funções listadas no [funções escalares do apêndice e:](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obter mais informações sobre a sequência de escape de função escalar, consulte [sequência de Escape de função escalar](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) na gramática do apêndice c: SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados do cliente maiusculas nomes. A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe de nativo para Ingres para OS/2 e não é interoperável.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Um aplicativo pode misturar chamadas para funções escalares que usam sintaxe nativo e chamadas para funções escalares que usam sintaxe ODBC. Por exemplo, suponha que os nomes na tabela de funcionários são armazenados como um sobrenome, uma vírgula e um nome. A instrução SQL a seguir cria um conjunto de resultados de sobrenomes de funcionários na tabela de funcionários. A instrução usa a função escalar ODBC **subcadeia de caracteres** e a função escalar do SQL Server **CHARINDEX** e serão executados corretamente apenas no SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) – 1)} FROM Customers  
```  
  
 Para interoperabilidade máxima, os aplicativos devem usar o **converter** função escalar para certificar-se de que a saída de uma função escalar é o tipo exigido. O **converter** função converte dados de um tipo de dados do SQL para o tipo de dados SQL especificado. A sintaxe do **converter** função é  
  
 **Converter (** *value_exp* **,** *data_type***)**  
  
 onde *value_exp* é um nome de coluna, o resultado de outra função escalar ou um valor literal, e *data_type* é uma palavra-chave que corresponde a **#define** nome que é usado por um Identificador de tipo de dados SQL conforme definido em [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md). Por exemplo, a instrução SQL a seguir usa o **converter** função para certificar-se de que a saída do **CURDATE** função for uma data, em vez de um caractere ou carimbo de hora de dados:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar quais funções escalares têm suporte por uma fonte de dados, um aplicativo chama **SQLGetInfo** com SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS e SQL_TIMEDATE_ Opções de funções. Para determinar quais operações de conversão são suportadas pelo **converter** função, um aplicativo chama **SQLGetInfo** com qualquer uma das opções que começam com SQL_CONVERT.
