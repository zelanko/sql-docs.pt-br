---
title: "Conversão de dados do SQL para tipos de dados C | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8fae054b572cb0d61299781d67adc0038afa9a97
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="converting-data-from-sql-to-c-data-types"></a>Conversão de dados do SQL para tipos de dados C
Quando um aplicativo chama **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData**, o driver recupera os dados da fonte de dados. Se necessário, ele converte os dados do tipo de dados no qual o driver recuperá-lo para o tipo de dados especificado pelo *TargetType* argumento **SQLBindCol** ou **SQLGetData.** Finalmente, ele armazena os dados no local apontado pelo *TargetValuePtr* argumento **SQLBindCol** ou **SQLGetData** (e o campo SQL_DESC_DATA_PTR da descartar).  
  
 A tabela a seguir mostra as conversões com suporte do ODBC SQL tipos de dados para tipos de dados ODBC C. Um círculo preenchido indica a conversão padrão para um tipo de dados SQL (o tipo de dados C para o qual os dados serão convertidos quando o valor de *TargetType* é SQL_C_DEFAULT). Um círculo vazio indica uma conversão com suporte.  
  
 Para um ODBC 3*. x* aplicativo trabalhando com um ODBC 2.* x* driver, conversão de dados específica do driver tipos podem não ter suporte.  
  
 O formato dos dados convertidos não é afetado pela configuração de país Windows®.  
  
 As tabelas nas seções a seguir descrevem como o driver ou fonte de dados converte os dados recuperados da fonte de dados; drivers são necessários para dar suporte a conversões para todos os tipos de dados ODBC C dos tipos de dados SQL ODBC que dão suporte a eles. Para um determinado tipo de dados SQL ODBC, a primeira coluna da tabela lista os valores válidos de entrada do *TargetType* argumento **SQLBindCol** e **SQLGetData**. A segunda coluna lista os resultados de um teste, geralmente usando o *BufferLength* argumento especificado em **SQLBindCol** ou **SQLGetData**, que o driver executa a Determine se ele pode converter os dados. Para cada resultado, as terceira e quarta colunas listam os valores colocados nos buffers especificados pelo *TargetValuePtr* e *StrLen_or_IndPtr* argumentos especificados na **SQLBindCol** ou **SQLGetData** depois que o driver tentou converter os dados. (O *StrLen_or_IndPtr* argumento corresponde ao campo SQL_DESC_OCTET_LENGTH_PTR da descartar.) A última coluna lista o SQLSTATE retornado para cada resultado por **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData**.  
  
 Se o *TargetType* argumento **SQLBindCol** ou **SQLGetData** contém um identificador para um tipo de dados ODBC C não mostrado na tabela para um determinado tipo de dados SQL ODBC ** SQLFetch**, **SQLFetchScroll**, ou **SQLGetData** retornará SQLSTATE 07006 (violação do atributo de tipo de dados restrito). Se o *TargetType* argumento contém um identificador que especifica uma conversão de um tipo de dados SQL específico do driver para um tipo de dados ODBC C e esta conversão não é suportada pelo driver, **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData** retornará SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Embora não seja mostrado nas tabelas, o driver retorna SQL_NULL_DATA no buffer especificado pelo *StrLen_or_IndPtr* argumento quando o valor de dados SQL é NULL. Para obter uma explicação sobre o uso de *StrLen_or_IndPtr* quando várias chamadas são feitas para recuperar dados, consulte o [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)descrição da função. Quando dados do SQL são convertidos em dados de caractere C, o número de caracteres retornados na \* *StrLen_or_IndPtr* não inclui o byte nulo de terminação. Se *TargetValuePtr* é um ponteiro nulo, **SQLGetData** retorna SQLSTATE HY009 (uso inválido de ponteiro nulo); na **SQLBindCol**, isso desvincula a coluna.  
  
 Os termos e as convenções a seguir são usadas nas tabelas:  
  
-   **Comprimento em bytes de dados** é o número de bytes de dados de C disponíveis para retornar em **TargetValuePtr*, se os dados serão truncados antes de ser retornado para o aplicativo ou não. Para dados de cadeia de caracteres, isso não inclui o espaço para o caractere null de terminação.  
  
-   **Bytes de comprimento de caracteres** é o número total de bytes necessários para exibir os dados em formato de caractere. Isso é definido para cada tipo de dados C na seção [exibir tamanho](../../../odbc/reference/appendixes/display-size.md), exceto que o comprimento de bytes de caractere é em bytes, enquanto o tamanho de exibição está em caracteres.  
  
-   As palavras em *itálico* representar argumentos de função ou elementos da gramática SQL. Para obter a sintaxe de elementos de gramática, consulte [gramática de SQL do apêndice c:](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [SQL to C: caractere](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL to C: numérico](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL to C: bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL to C: binário](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL to C: data](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL to C: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL to C: hora](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL to C: carimbo de data/hora](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL to C: intervalos de ano-mês](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL to C: intervalos de tempo-dia](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [Exemplos de conversão de dados SQL to C](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
