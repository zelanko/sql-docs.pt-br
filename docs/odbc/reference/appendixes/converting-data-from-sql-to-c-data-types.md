---
title: Conversão de dados de SQL para Tipos de Dados C | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284746"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Converter dados de SQL para tipos de dados do C
Quando um aplicativo chama **SQLFetch,** **SQLFetchScroll**ou **SQLGetData,** o driver recupera os dados da fonte de dados. Se necessário, ele converte os dados do tipo de dados no qual o driver os recuperou para o tipo de dados especificado pelo argumento *TargetType* no **SQLBindCol** ou **SQLGetData.** Finalmente, ele armazena os dados na localização apontada pelo argumento *TargetValuePtr* no **SQLBindCol** ou **SQLGetData** (e no campo SQL_DESC_DATA_PTR do ARD).  
  
 A tabela a seguir mostra as conversões suportadas dos tipos de dados ODBC SQL para os tipos de dados ODBC C. Um círculo preenchido indica a conversão padrão para um tipo de dados SQL (o tipo de dados C para o qual os dados serão convertidos quando o valor do *TargetType* é SQL_C_DEFAULT). Um círculo oco indica uma conversão suportada.  
  
 Para um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x,* a conversão de tipos de dados específicos do driver pode não ser suportada.  
  
 O formato dos dados convertidos não é afetado pela configuração de país ® Windows.  
  
 As tabelas nas seções a seguir descrevem como o driver ou a fonte de dados converte dados recuperados da fonte de dados; os drivers são necessários para suportar conversões para todos os tipos de dados ODBC C dos tipos de dados SQL do ODBC que eles suportam. Para um determinado tipo de dados SQL do ODBC, a primeira coluna da tabela lista os valores de entrada legal do argumento *TargetType* no **SQLBindCol** e **no SQLGetData**. A segunda coluna lista os resultados de um teste, muitas vezes usando o argumento *BufferLength* especificado no **SQLBindCol** ou **SQLGetData**, que o driver executa para determinar se ele pode converter os dados. Para cada resultado, a terceira e quarta colunas listam os valores colocados nos buffers especificados pelo *TargetValuePtr* e *StrLen_or_IndPtr* argumentos especificados no **SQLBindCol** ou **SQLGetData** após o driver tentar converter os dados. (O *argumento StrLen_or_IndPtr* corresponde ao campo SQL_DESC_OCTET_LENGTH_PTR da ARD.) A última coluna lista o SQLSTATE retornado para cada resultado por **SQLFetch,** **SQLFetchScroll**ou **SQLGetData**.  
  
 Se o argumento *TargetType* no **SQLBindCol** ou **no SQLGetData** contiver um identificador para um tipo de dados ODBC C não mostrado na tabela para um determinado tipo de dados SQL ODBC, **SQLFetch,** **SQLFetchScroll**ou **SQLGetData** retorna SQLSTATE 07006 (violação de atributo de tipo de dados restrito). Se o argumento *TargetType* contiver um identificador que especifica uma conversão de um tipo de dados SQL específico para um driver para um tipo de dados ODBC C e essa conversão não for suportada pelo driver, **SQLFetch,** **SQLFetchScroll**ou **SQLGetData** retorna SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Embora não seja mostrado nas tabelas, o driver retorna SQL_NULL_DATA no buffer especificado pelo *argumento StrLen_or_IndPtr* quando o valor dos dados SQL é NULO. Para obter uma explicação sobre o uso de *StrLen_or_IndPtr* quando várias chamadas são feitas para recuperar dados, consulte a descrição da função [SQLGetData.](../../../odbc/reference/syntax/sqlgetdata-function.md) Quando os dados SQL são convertidos em dados \*do caractere C, a contagem de caracteres retornada em *StrLen_or_IndPtr* não inclui o byte de rescisão nula. Se *o TargetValuePtr* for um ponteiro nulo, **o SQLGetData** retorna o SQLSTATE HY009 (uso inválido do ponteiro nulo); em **SQLBindCol**, isso desvincula a coluna.  
  
 Os seguintes termos e convenções são usados nas tabelas:  
  
-   **Byte comprimento de dados** é o número de bytes de dados C disponíveis para retornar em **TargetValuePtr*, se os dados serão truncados antes de serem devolvidos ao aplicativo. Para dados de seqüência, isso não inclui o espaço para o caractere de rescisão nula.  
  
-   **Comprimento de byte de caractere** é o número total de bytes necessários para exibir os dados em formato de caractere. Isso é definido como definido para cada tipo de dados C na seção Tamanho de [exibição,](../../../odbc/reference/appendixes/display-size.md)exceto que o comprimento do byte do caractere está em bytes enquanto o tamanho do display está em caracteres.  
  
-   Palavras em *itálico* representam argumentos de função ou elementos da gramática SQL. Para a sintaxe dos elementos gramaticais, consulte [apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
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
