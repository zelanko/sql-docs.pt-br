---
title: Conversão de dados de C para tipos de dados SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fb707e77df7d793277d4a23146adc980eede6fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304655"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>Converter dados de C para tipos de dados SQL
Quando um aplicativo chama **SQLExecute** ou **SQLExecDirect,** o driver recupera os dados para quaisquer parâmetros vinculados ao **SQLBindParameter** a partir de locais de armazenamento no aplicativo. Quando um aplicativo chama **SQLSetPos,** o driver recupera os dados para uma atualização ou adiciona operação a partir de colunas vinculadas ao **SQLBindCol**. Para parâmetros de data-at-execution, o aplicativo envia os dados de parâmetros com **SQLPutData**. Se necessário, o driver converte os dados do tipo de dados especificado pelo argumento *ValueType* no **SQLBindParameter** para o tipo de dados especificado pelo argumento *ParameterType* no **SQLBindParameter**e, em seguida, envia os dados para a fonte de dados.  
  
 A tabela a seguir mostra as conversões suportadas dos tipos de dados ODBC C para os tipos de dados ODBC SQL. Um círculo preenchido indica a conversão padrão para um tipo de dados SQL (o tipo de dados C do qual os dados serão convertidos quando o valor do *ValueType* ou do campo de descritor SQL_DESC_CONCISE_TYPE for SQL_C_DEFAULT). Um círculo oco indica uma conversão suportada.  
  
 O formato dos dados convertidos não é afetado pela configuração de país ® Windows.  
  
 ![Conversões suportadas: tipos de dados ODBC C em SQL](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 As tabelas nas seções a seguir descrevem como o driver ou a fonte de dados converte dados enviados à fonte de dados; os drivers são necessários para suportar conversões de todos os tipos de dados ODBC C para os tipos de dados SQL ODBC que eles suportam. Para um determinado tipo de dados ODBC C, a primeira coluna da tabela lista os valores de entrada legais do argumento *ParameterType* no **SQLBindParameter**. A segunda coluna lista os resultados de um teste que o driver realiza para determinar se ele pode converter os dados. A terceira coluna lista o SQLSTATE retornado para cada resultado por **SQLExecDirect,** **SQLExecute,** **SQLBulkOperations,** **SQLSetPos**ou **SQLPutData**. Os dados são enviados à fonte de dados somente se SQL_SUCCESS for devolvido.  
  
 Se o argumento *ParameterType* no **SQLBindParameter** contiver o identificador de um tipo de dados ODBC SQL que não é mostrado na tabela para um determinado tipo de dados C, **O SQLBindParameter** retorna SQLSTATE 07006 (violação de atributo tipo de dados restrito). Se o argumento *ParameterType* contiver um identificador específico do driver e o driver não suportar a conversão do tipo de dados Específico do ODBC C para esse tipo de dados SQL específico do driver, **o SQLBindParameter** retorna o SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Se os argumentos *ParameterValuePtr* e *StrLen_or_IndPtr* especificados no **SQLBindParameter** forem ambos ponteiros nulos, essa função retorna SQLSTATE HY009 (uso inválido do ponteiro nulo). Embora não seja mostrado nas tabelas, um aplicativo define o valor do buffer comprimento/indicador apontado pelo *argumento StrLen_or_IndPtr* do **SQLBindParameter** ou o valor do argumento *StrLen_or_IndPtr* do **SQLPutData** para SQL_NULL_DATA especificar um valor de dados SQL NULO. (O *argumento StrLen_or_IndPtr* corresponde ao campo SQL_DESC_OCTET_LENGTH_PTR da APD.) O aplicativo define esses valores para \*SQL_NTS especificar que o valor em \* *ParameterValuePtr* no **SQLBindParameter** ou *DataPtr* no **SQLPutData** (apontado pelo campo SQL_DESC_DATA_PTR da APD) é uma seqüência de terminadas por nulidade.  
  
 Os seguintes termos são usados nas tabelas:  
  
-   **Byte de comprimento de dados** - Número de bytes de dados SQL disponíveis para enviar à fonte de dados, se os dados serão truncados antes de serem enviados para a fonte de dados. Para dados de seqüência, isso não inclui espaço para o caractere de rescisão nula.  
  
-   **Comprimento do byte** da coluna - Número de bytes necessários para armazenar os dados na fonte de dados.  
  
-   **Comprimento do byte do** caractere - Número máximo de bytes necessários para exibir dados na forma de caractere. Isso é definido como definido para cada tipo de dados SQL no [Tamanho de exibição,](../../../odbc/reference/appendixes/display-size.md)exceto que o comprimento do byte de caracteres está em bytes, enquanto o tamanho do display está em caracteres.  
  
-   **Número de dígitos** - Número de caracteres usados para representar um número, incluindo o sinal de menos, ponto decimal e expoente (se necessário).  
  
-   **Palavras em**   
     ***itálico*** - Elementos da gramática SQL. Para a sintaxe dos elementos gramaticais, consulte [apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [C to SQL: caractere](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C to SQL: numérico](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C to SQL: bit](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C to SQL: binário](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C to SQL: data](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C to SQL: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C to SQL: hora](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C to SQL: carimbo de data/hora](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C to SQL: intervalos de ano-mês](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C to SQL: intervalos de tempo-dia](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [Exemplos de conversão de dados C to SQL](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
