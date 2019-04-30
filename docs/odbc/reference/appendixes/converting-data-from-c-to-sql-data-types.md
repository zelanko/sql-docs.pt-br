---
title: Convertendo dados de C para tipos de dados SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 168fa55d89488277cd17f4bdca3105f7d879c8f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224666"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>Converter dados de C para tipos de dados SQL
Quando um aplicativo chama **SQLExecute** ou **SQLExecDirect**, o driver recupera os dados para quaisquer parâmetros associados com **SQLBindParameter** nos locais de armazenamento em o aplicativo. Quando um aplicativo chama **SQLSetPos**, o driver recupera os dados para uma atualização ou operação de adição de colunas associadas **SQLBindCol**. Para parâmetros de dados em execução, o aplicativo envia os dados de parâmetro com **SQLPutData**. Se necessário, o driver converterá os dados do tipo de dados especificado pela *ValueType* argumento na **SQLBindParameter** para o tipo de dados especificado pelo *ParameterType*argumento na **SQLBindParameter**e, em seguida, envia os dados para a fonte de dados.  
  
 A tabela a seguir mostra as conversões com suporte do ODBC C em tipos de dados para tipos de dados SQL ODBC. Um círculo preenchido indica a conversão padrão para um tipo de dados SQL (o tipo de dados C da qual os dados serão convertidos quando o valor de *ValueType* ou o campo do descritor SQL_DESC_CONCISE_TYPE for SQL_C_DEFAULT). Um círculo vazio indica uma conversão com suporte.  
  
 O formato dos dados convertidos não é afetado pela configuração de país Windows®.  
  
 ![Conversões com suporte: ODBC C para tipos de dados SQL](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 As tabelas nas seções a seguir descrevem como o driver ou fonte de dados converte os dados enviados para a fonte de dados; drivers são necessários para dar suporte a conversões de todos os tipos de dados ODBC C para os tipos de dados SQL ODBC que dão suporte a eles. Para um determinado tipo de dados ODBC C, a primeira coluna da tabela lista os valores de entrada válidos do *ParameterType* argumento **SQLBindParameter**. A segunda coluna lista os resultados de um teste que o driver executa para determinar se ele pode converter os dados. A terceira coluna lista o SQLSTATE retornado para cada resultado por **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, **SQLSetPos**, ou **SQLPutData**. Dados são enviados à fonte de dados somente se SQL_SUCCESS for retornado.  
  
 Se o *ParameterType* argumento **SQLBindParameter** contém o identificador de um tipo de dados SQL ODBC que não seja mostrado na tabela para um determinado tipo de dados C **SQLBindParameter**retorna um SQLSTATE 07006 (violação do atributo de tipo de dados restrito). Se o *ParameterType* argumento contém um identificador específico do driver e o driver não oferece suporte para a conversão de tipo de dados ODBC C específico para esse tipo de dados SQL específico do driver, **SQLBindParameter** retorna um SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Se o *ParameterValuePtr* e *StrLen_or_IndPtr* argumentos especificados na **SQLBindParameter** são ambos ponteiros nulos, que a função retornará SQLSTATE HY009 (inválido o uso de ponteiro nulo). Embora não seja mostrado nas tabelas, um aplicativo define o valor do buffer de comprimento/indicador apontado para o *StrLen_or_IndPtr* argumento de **SQLBindParameter** ou o valor da  *StrLen_or_IndPtr* argumento de **SQLPutData** como SQL_NULL_DATA para especificar um valor de dados SQL NULL. (O *StrLen_or_IndPtr* argumento corresponde ao campo SQL_DESC_OCTET_LENGTH_PTR de APD.) O aplicativo define esses valores como SQL_NTS para especificar que o valor \* *ParameterValuePtr* na **SQLBindParameter** ou \* *DataPtr*na **SQLPutData** (apontando para o campo SQL_DESC_DATA_PTR de APD) é uma cadeia de caracteres terminada em nulo.  
  
 Os seguintes termos são usados nas tabelas:  
  
-   **Comprimento de bytes dos dados** - número de bytes de dados do SQL enviar para a fonte de dados, ou não os dados serão truncados antes de serem enviado à fonte de dados. Para dados de cadeia de caracteres, isso não inclui espaço para o caractere nulo de terminação.  
  
-   **Comprimento de bytes da coluna** -número de bytes necessários para armazenar os dados na fonte de dados.  
  
-   **Bytes de comprimento de caracteres** - máximo número de bytes necessários para exibir dados em formato de caractere. Isso é, conforme definido para cada tipo de dados SQL no [exibir tamanho](../../../odbc/reference/appendixes/display-size.md), exceto o comprimento de byte do caractere está em bytes, e o tamanho da exibição está em caracteres.  
  
-   **Número de dígitos** - número de caracteres usados para representar um número, incluindo o sinal de subtração, o ponto decimal e o expoente (se necessário).  
  
-   **Palavras em**   
     ***Itálico*** -elementos da gramática SQL. Para obter a sintaxe de elementos de gramática, consulte [apêndice c: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [C to SQL: Caractere](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C to SQL: numérico](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C to SQL: Bit](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C to SQL: binário](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C to SQL: Data](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C to SQL: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C to SQL: tempo](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C to SQL: Timestamp](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C to SQL: Intervalos de ano / mês](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C to SQL: Intervalos de tempo do dia](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [Exemplos de conversão de dados C to SQL](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
