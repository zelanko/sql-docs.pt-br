---
title: Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência, tamanho da exibição | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306567"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho da tela - ODBC
Os tipos de dados são caracterizados pelo tamanho da coluna (ou parâmetro), dígitos decimais, comprimento e tamanho do display. As funções ODBC a seguir retornam esses atributos para um parâmetro em uma declaração SQL ou para um tipo de dados SQL em uma fonte de dados. Cada função ODBC retorna um conjunto diferente desses atributos, da seguinte forma:  
  
-   **SQLDescribeCol** retorna o tamanho da coluna e os dígitos decimais das colunas que descreve.  
  
-   **SQLDescribeParam** retorna o tamanho do parâmetro e os dígitos decimais dos parâmetros que descreve. **SQLBindParameter** define o tamanho do parâmetro e os dígitos decimais para um parâmetro em uma declaração SQL.  
  
-   O catálogo funciona **com sqlcolumns,** **sqlprocedurecolumns**e atributos de retorno **SQLGetTypeInfo** para uma coluna em uma tabela, conjunto de resultados ou um parâmetro de procedimento e os atributos de catálogo dos tipos de dados na fonte de dados. **SQLColumns** retorna o tamanho da coluna, os dígitos decimais e o comprimento de uma coluna em tabelas especificadas (como a tabela base, exibição ou uma tabela do sistema). **SQLProcedureColunas** retorna o tamanho da coluna, os dígitos decimais e o comprimento de uma coluna em um procedimento. **O SQLGetTypeInfo** retorna o tamanho máximo da coluna e os dígitos decimais mínimos e máximos de um tipo de dados SQL em uma fonte de dados.  
  
 Os valores retornados por essas funções para o tamanho da coluna ou do parâmetro correspondem a "precisão" conforme definido no ODBC 2. *x*. No entanto, os valores não correspondem necessariamente aos valores devolvidos em SQL_DESC_PRECISION ou qualquer outro campo descritor. O mesmo vale para dígitos decimais, que correspondem a "escala" conforme definido em ODBC 2. *x*. Não corresponde necessariamente aos valores devolvidos em SQL_DESC_SCALE ou qualquer outro campo descritor, mas vem de diferentes campos descritores, dependendo do tipo de dados. Para obter mais informações, consulte [Tamanho da coluna](../../../odbc/reference/appendixes/column-size.md) e [dígitos decimais](../../../odbc/reference/appendixes/decimal-digits.md).  
  
 Da mesma forma, os valores para o comprimento do octeto de transferência não vêm de SQL_DESC_LENGTH. Eles vêm do SQL_DESC_OCTET_LENGTH de um campo de um descritor para todos os tipos de caracteres e binários. Não há campo descritor que detenha essas informações para outros tipos.  
  
 O valor do tamanho do display para todos os tipos de dados corresponde ao valor em um único campo descritor, SQL_DESC_DISPLAY_SIZE.  
  
 Os campos descritores descrevem as características de um conjunto de resultados. Os campos descritores não contêm valores válidos sobre os dados antes da execução da declaração. Os valores para tamanho da coluna, dígitos decimais e tamanho de exibição retornados por **SQLColumns,** **SQLProcedureColumns**e **SQLGetTypeInfo,** por outro lado, retornam características de objetos de banco de dados, como colunas de tabela e tipos de dados, que existem no catálogo da fonte de dados. Da mesma forma, em seu conjunto de resultados, **SQLColAttribute** retorna o tamanho da coluna, os dígitos decimais e o comprimento do octeto de transferência de colunas na fonte de dados; esses valores não são necessariamente os mesmos dos valores nos campos SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_OCTET_LENGTH descritores.  
  
 Para obter mais informações sobre esses campos de descritores, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Tópicos relacionados:  
  
-   [Tamanho da coluna](../../../odbc/reference/appendixes/column-size.md)  
-   [Dígitos decimais](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [Comprimento do octeto de transferência](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [Tamanho de exibição](../../../odbc/reference/appendixes/display-size.md)
