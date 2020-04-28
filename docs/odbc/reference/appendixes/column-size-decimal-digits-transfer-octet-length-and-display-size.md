---
title: Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência, tamanho de exibição | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55b8e9dd305764a89601e9ffd5a337e42a8d8db3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306567"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição-ODBC
Os tipos de dados são caracterizados por seu tamanho de coluna (ou parâmetro), dígitos decimais, comprimento e tamanho de exibição. As seguintes funções ODBC retornam esses atributos para um parâmetro em uma instrução SQL ou para um tipo de dados SQL em uma fonte de dados. Cada função ODBC retorna um conjunto diferente desses atributos, da seguinte maneira:  
  
-   **SQLDescribeCol** retorna o tamanho da coluna e os dígitos decimais das colunas que ele descreve.  
  
-   **SQLDescribeParam** retorna o tamanho do parâmetro e os dígitos decimais dos parâmetros que ele descreve. **SQLBindParameter** define o tamanho do parâmetro e os dígitos decimais para um parâmetro em uma instrução SQL.  
  
-   As funções de catálogo **SQLColumns**, **SQLProcedureColumns**e **SQLGetTypeInfo** retornam atributos para uma coluna em uma tabela, um conjunto de resultados ou um parâmetro de procedimento e os atributos de catálogo dos tipos de dados na fonte de dados. **SQLColumns** retorna o tamanho da coluna, os dígitos decimais e o comprimento de uma coluna em tabelas especificadas (como a tabela base, a exibição ou uma tabela do sistema). **SQLProcedureColumns** retorna o tamanho da coluna, os dígitos decimais e o comprimento de uma coluna em um procedimento. **SQLGetTypeInfo** retorna o tamanho máximo da coluna e os dígitos decimais mínimo e máximo de um tipo de dados SQL em uma fonte de dados.  
  
 Os valores retornados por essas funções para o tamanho de coluna ou parâmetro correspondem a "precisão", conforme definido no ODBC 2. *x*. No entanto, os valores não correspondem necessariamente aos valores retornados em SQL_DESC_PRECISION ou em qualquer outro campo de descritor. O mesmo é verdadeiro para dígitos decimais, que correspondem a "escala", conforme definido no ODBC 2. *x*. Ele não corresponde necessariamente aos valores retornados em SQL_DESC_SCALE ou em qualquer outro campo de descritor, mas vem de campos de descritor diferentes, dependendo do tipo de dados. Para obter mais informações, consulte [tamanho da coluna](../../../odbc/reference/appendixes/column-size.md) e [dígitos decimais](../../../odbc/reference/appendixes/decimal-digits.md).  
  
 Da mesma forma, os valores para o comprimento do octeto de transferência não são provenientes de SQL_DESC_LENGTH. Elas são provenientes da SQL_DESC_OCTET_LENGTH de um campo de um descritor para todos os tipos de caracteres e binários. Não há nenhum campo de descritor que contém essas informações para outros tipos.  
  
 O valor de tamanho de exibição para todos os tipos de dados corresponde ao valor em um único campo de descritor, SQL_DESC_DISPLAY_SIZE.  
  
 Os campos de descritor descrevem as características de um conjunto de resultados. Os campos de descritor não contêm valores válidos sobre os dados antes da execução da instrução. Os valores para tamanho de coluna, dígitos decimais e tamanho de exibição retornados por **SQLColumns**, **SQLProcedureColumns**e **SQLGetTypeInfo**, por outro lado, retornam características de objetos de banco de dados, como colunas de tabela e tipos de dado, que existem no catálogo da fonte de dados. Da mesma forma, em seu conjunto de resultados, **SQLColAttribute** retorna o tamanho da coluna, os dígitos decimais e o comprimento do octeto de transferência de colunas na fonte de dados; esses valores não são necessariamente os mesmos que os valores nos campos SQL_DESC_PRECISION, SQL_DESC_SCALE e descritor SQL_DESC_OCTET_LENGTH.  
  
 Para obter mais informações sobre esses campos de descritor, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Tópicos relacionados:  
  
-   [Tamanho da coluna](../../../odbc/reference/appendixes/column-size.md)  
-   [Dígitos decimais](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [Comprimento do octeto de transferência](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [Tamanho de exibição](../../../odbc/reference/appendixes/display-size.md)
