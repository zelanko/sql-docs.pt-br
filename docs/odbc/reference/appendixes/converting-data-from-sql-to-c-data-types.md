---
title: Convertendo dados de SQL para tipos de dados C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 553596f474cd8e7c4f4c91911b0167d5b1bc0b4a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224478"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Converter dados de SQL para tipos de dados do C
Quando um aplicativo chama **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData**, o driver recupera os dados da fonte de dados. Se necessário, ele converte os dados do tipo de dados em que o driver recuperados-lo para o tipo de dados especificado pela *TargetType* argumento **SQLBindCol** ou **SQLGetData.** Por fim, ele armazena os dados no local apontado pela *TargetValuePtr* argumento **SQLBindCol** ou **SQLGetData** (e o campo SQL_DESC_DATA_PTR da descartar).  
  
 A tabela a seguir mostra as conversões com suporte do ODBC SQL em tipos de dados para tipos de dados ODBC C. Um círculo preenchido indica a conversão padrão para um tipo de dados SQL (o tipo de dados C para o qual os dados serão convertidos quando o valor de *TargetType* é SQL_C_DEFAULT). Um círculo vazio indica uma conversão com suporte.  
  
 Para um ODBC 3 *. x* aplicativo trabalhar com um ODBC 2. *x* driver, a conversão de dados específica do driver tipos podem não ter suporte.  
  
 O formato dos dados convertidos não é afetado pela configuração de país Windows®.  
  
 As tabelas nas seções a seguir descrevem como o driver ou fonte de dados converte os dados recuperados da fonte de dados; drivers são necessários para dar suporte a conversões para todos os tipos de dados ODBC C dos tipos de dados SQL ODBC que dão suporte a eles. Para um determinado tipo de dados SQL ODBC, a primeira coluna da tabela lista os valores válidos de entrada do *TargetType* argumento **SQLBindCol** e **SQLGetData**. A segunda coluna lista os resultados de um teste, geralmente usando o *BufferLength* argumento especificado em **SQLBindCol** ou **SQLGetData**, que o driver executa a Determine se ele pode converter os dados. Para cada resultado, as terceira e quarta colunas listam os valores colocados nos buffers especificados pelo *TargetValuePtr* e *StrLen_or_IndPtr* argumentos especificados na **SQLBindCol** ou **SQLGetData** depois que o driver tentou converter os dados. (O *StrLen_or_IndPtr* argumento corresponde ao campo SQL_DESC_OCTET_LENGTH_PTR da descartar.) A última coluna lista o SQLSTATE retornado para cada resultado por **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData**.  
  
 Se o *TargetType* argumento **SQLBindCol** ou **SQLGetData** contém um identificador para um tipo de dados ODBC C não mostrado na tabela para um determinado tipo de dados SQL ODBC  **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData** retornará SQLSTATE 07006 (violação do atributo de tipo de dados restrito). Se o *TargetType* argumento contém um identificador que especifica uma conversão de um tipo de dados específicos do driver SQL de um tipo de dados ODBC C e não tem suporte pelo driver, essa conversão **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData** retornará SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Embora não seja mostrado nas tabelas, o driver retorna SQL_NULL_DATA no buffer especificado pelo *StrLen_or_IndPtr* argumento quando o valor de dados SQL é NULL. Para obter uma explicação do uso de *StrLen_or_IndPtr* quando várias chamadas são feitas para recuperar dados, consulte o [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)descrição da função. Quando os dados SQL são convertidos em dados de caractere C, a contagem de caracteres retornado em \* *StrLen_or_IndPtr* não inclui o byte nulo de terminação. Se *TargetValuePtr* for um ponteiro nulo, **SQLGetData** retorna um SQLSTATE HY009 (uso inválido de ponteiro nulo); na **SQLBindCol**, isso desvincula a coluna.  
  
 Os termos e as convenções a seguir são usadas nas tabelas:  
  
-   **Comprimento de bytes de dados** é o número de bytes de dados C disponíveis para retornar em **TargetValuePtr*, esteja ou não os dados serão truncados antes de ser retornado ao aplicativo. Para dados de cadeia de caracteres, isso não inclui o espaço para o caractere nulo de terminação.  
  
-   **Bytes de comprimento de caracteres** é o número total de bytes necessários para exibir os dados em formato de caractere. Isso é, conforme definido para cada tipo de dados C na seção [exibir tamanho](../../../odbc/reference/appendixes/display-size.md), exceto que o comprimento de byte do caractere está em bytes e o tamanho da exibição está em caracteres.  
  
-   Palavras *itálico* representam argumentos de função ou elementos de gramática SQL. Para obter a sintaxe de elementos de gramática, consulte [apêndice c: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [SQL para c: Caractere](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL para c: numérico](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL para c: Bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL para c: binário](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL para c: Data](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL para c: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL para c: tempo](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL para c: Timestamp](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL para c: Intervalos de ano / mês](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL para c: Intervalos de tempo do dia](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [Exemplos de conversão de dados SQL to C](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
