---
title: Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência, o tamanho de exibição | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8d7f1b8ec5647a34b09f0636fc8fcc2ad070f72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019245"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e exibir tamanho - ODBC
Tipos de dados são caracterizados por tamanho de coluna (ou parâmetro), dígitos decimais, comprimento e tamanho de exibição. As seguintes funções ODBC retornam esses atributos para um parâmetro em uma instrução SQL ou para um tipo de dados SQL em uma fonte de dados. Cada função ODBC retorna um conjunto diferente desses atributos, da seguinte maneira:  
  
-   **SQLDescribeCol** retorna a coluna de dígitos decimal e tamanho das colunas que ele descreve.  
  
-   **SQLDescribeParam** retorna o parâmetro de dígitos decimal e tamanho dos parâmetros que ele descreve. **SQLBindParameter** define o parâmetro de dígitos decimal e tamanho para um parâmetro em uma instrução SQL.  
  
-   As funções de catálogo **SQLColumns**, **SQLProcedureColumns**, e **SQLGetTypeInfo** retornar atributos para uma coluna em uma tabela, o conjunto de resultados ou um parâmetro de procedimento e os atributos de catálogo dos tipos de dados na fonte de dados. **SQLColumns** retorna o tamanho da coluna, dígitos decimais e comprimento de uma coluna em tabelas especificadas (por exemplo, a tabela base, exibição ou uma tabela do sistema). **SQLProcedureColumns** retorna o tamanho da coluna, dígitos decimais e comprimento de uma coluna em um procedimento. **SQLGetTypeInfo** retorna o tamanho máximo da coluna e os dígitos decimais mínimos e máximo de um tipo de dados SQL em uma fonte de dados.  
  
 Os valores retornados por essas funções para a coluna ou o tamanho de parâmetro correspondem a "precisão" conforme definido no ODBC 2. *x*. No entanto, os valores não necessariamente correspondem aos valores retornados em SQL_DESC_PRECISION ou qualquer outro campo de descritor um. O mesmo é verdadeiro para dígitos decimais, que correspondem aos "escala" como definida no ODBC 2. *x*. Ele não necessariamente corresponde aos valores retornados em SQL_DESC_SCALE ou qualquer outro campo de descritor um, mas vem de campos de descritor diferente dependendo do tipo de dados. Para obter mais informações, consulte [tamanho da coluna](../../../odbc/reference/appendixes/column-size.md) e [dígitos decimais](../../../odbc/reference/appendixes/decimal-digits.md).  
  
 Da mesma forma, os valores para o comprimento do octeto de transferência não vêm da SQL_DESC_LENGTH. Eles são provenientes de SQL_DESC_OCTET_LENGTH de um campo de um descritor para todos os caracteres e tipos binários. Não há nenhum campo de descritor que contém essas informações para outros tipos.  
  
 O valor de tamanho de exibição para todos os tipos de dados corresponde ao valor em um campo de descritor único, colunas de SQL_DESC_DISPLAY_SIZE.  
  
 Campos de descritor descrevem as características de um conjunto de resultados. Campos de descritor não contêm valores válidos sobre dados antes da execução da instrução. Os valores de coluna de tamanho, dígitos decimais e exibir o tamanho retornado por **SQLColumns**, **SQLProcedureColumns**, e **SQLGetTypeInfo**, por outro lado, retornar características de objetos de banco de dados, como colunas de tabela e tipos de dados, que existe no catálogo da fonte de dados. Da mesma forma, no seu conjunto de resultados **SQLColAttribute** retorna o tamanho da coluna, dígitos decimais e comprimento do octeto de transferência de colunas na fonte de dados; esses valores não são necessariamente os mesmos que os valores no SQL_DESC_PRECISION, SQL _ DESC_SCALE e campos de descritor SQL_DESC_OCTET_LENGTH.  
  
 Para obter mais informações sobre esses campos de descritor, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Tópicos relacionados:  
  
-   [Tamanho da coluna](../../../odbc/reference/appendixes/column-size.md)  
-   [Dígitos decimais](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [Comprimento do octeto de transferência](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [Tamanho de exibição](../../../odbc/reference/appendixes/display-size.md)
