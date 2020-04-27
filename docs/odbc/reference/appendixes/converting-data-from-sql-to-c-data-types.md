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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a10730cb3910c55679c264583801cd57c83bfc3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284746"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Converter dados de SQL para tipos de dados do C
Quando um aplicativo chama **SQLFetch**, **SQLFetchScroll**ou **SQLGetData**, o driver recupera os dados da fonte de dados. Se necessário, ele converte os dados do tipo de dados no qual o driver o recuperou para o tipo de dados especificado pelo argumento *TargetType* em **SQLBindCol** ou **SQLGetData.** Por fim, ele armazena os dados no local apontado pelo argumento *TargetValuePtr* em **SQLBindCol** ou **SQLGetData** (e o campo SQL_DESC_DATA_PTR do ARD).  
  
 A tabela a seguir mostra as conversões com suporte de tipos de dados ODBC SQL para tipos de dados ODBC C. Um círculo preenchido indica a conversão padrão para um tipo de dados SQL (o tipo de dados C no qual os dados serão convertidos quando o valor de *TargetType* for SQL_C_DEFAULT). Um círculo vazio indica uma conversão com suporte.  
  
 Para um aplicativo ODBC *3. x* que trabalhe com um driver ODBC *2. x* , talvez não haja suporte para a conversão de tipos de dados específicos de driver.  
  
 O formato dos dados convertidos não é afetado pela configuração de país do Windows®.  
  
 As tabelas nas seções a seguir descrevem como o driver ou a fonte de dados converte os dados recuperados da fonte de dados; os drivers são necessários para dar suporte a conversões para todos os tipos de dados ODBC C dos tipos de dados ODBC SQL aos quais eles dão suporte. Para um determinado tipo de dados SQL ODBC, a primeira coluna da tabela lista os valores de entrada legais do argumento *TargetType* em **SQLBindCol** e **SQLGetData**. A segunda coluna lista os resultados de um teste, geralmente usando o argumento *BufferLength* especificado em **SQLBindCol** ou **SQLGetData**, que o driver executa para determinar se ele pode converter os dados. Para cada resultado, a terceira e a quarta colunas listam os valores colocados nos buffers especificados pelos argumentos *TargetValuePtr* e *StrLen_or_IndPtr* especificados em **SQLBindCol** ou **SQLGetData** depois que o driver tentou converter os dados. (O argumento *StrLen_or_IndPtr* corresponde ao campo SQL_DESC_OCTET_LENGTH_PTR do ARD.) A última coluna lista o SQLSTATE retornado para cada resultado por **SQLFetch**, **SQLFetchScroll**ou **SQLGetData**.  
  
 Se o argumento *TargetType* em **SQLBindCol** ou **SQLGetData** contiver um identificador para um tipo de dados ODBC C não mostrado na tabela para um determinado tipo de dados ODBC SQL, **SQLFetch**, **SQLFetchScroll**ou **SQLGetData** retornará SQLSTATE 07006 (violação de atributo de tipo de dados restrito). Se o argumento *TargetType* contiver um identificador que especifica uma conversão de um tipo de dados SQL específico de driver para um tipo de dados ODBC C e essa conversão não for suportada pelo driver, **SQLFetch**, **SQLFETCHSCROLL**ou **SQLGetData** retornará SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Embora não seja mostrado nas tabelas, o driver retorna SQL_NULL_DATA no buffer especificado pelo argumento *StrLen_or_IndPtr* quando o valor de dados SQL é nulo. Para obter uma explicação sobre o uso de *StrLen_or_IndPtr* quando várias chamadas são feitas para recuperar dados, consulte a descrição da função [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md). Quando os dados SQL são convertidos em dados de caractere C, a contagem \*de caracteres retornada em *StrLen_or_IndPtr* não inclui o byte de terminação nula. Se *TargetValuePtr* for um ponteiro nulo, **SQLGETDATA** retornará SQLSTATE HY009 (uso inválido de ponteiro nulo); no **SQLBindCol**, isso desassocia a coluna.  
  
 Os seguintes termos e convenções são usados nas tabelas:  
  
-   O **comprimento de bytes de dados** é o número de bytes de dados de C disponíveis para retornar em **TargetValuePtr*, se os dados serão truncados antes de serem retornados ao aplicativo. Para dados de cadeia de caracteres, isso não inclui o espaço para o caractere de terminação nula.  
  
-   **Comprimento de byte de caractere** é o número total de bytes necessários para exibir os dados no formato de caractere. Isso é conforme definido para cada tipo de dados C na seção [tamanho de exibição](../../../odbc/reference/appendixes/display-size.md), exceto que o comprimento de byte de caractere está em bytes, enquanto o tamanho de exibição está em caracteres.  
  
-   As palavras em *itálico* representam argumentos de função ou elementos da gramática SQL. Para obter a sintaxe dos elementos gramaticais, consulte o [Apêndice C: SQL Grammar](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta seção contém os seguintes tópicos.  
  
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
