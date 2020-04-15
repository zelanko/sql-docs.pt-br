---
title: Usando matrizes de parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b584dc3d635e9fa8ce3228e4e89b0f24451fe165
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306797"
---
# <a name="using-arrays-of-parameters"></a>Usar matrizes de parâmetros
Para usar matrizes de parâmetros, o aplicativo chama **SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_PARAMSET_SIZE para especificar o número de conjuntos de parâmetros. Ele chama **SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_PARAMS_PROCESSED_PTR para especificar o endereço de uma variável na qual o driver pode retornar o número de conjuntos de parâmetros processados, incluindo conjuntos de erros. Ele chama **SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_PARAM_STATUS_PTR apontar para uma matriz na qual retornar informações de status para cada linha de valores de parâmetro. O motorista armazena esses endereços na estrutura que mantém para a declaração.  
  
> [!NOTE]  
>  Em ODBC 2. *x*, **SQLParamOptions** foi chamado para especificar múltiplos valores para um parâmetro. Em ODBC 3. *x*, a chamada para **SQLParamOptions** foi substituída por chamadas para **SQLSetStmtAttr** para definir os atributos SQL_ATTR_PARAMSET_SIZE e SQL_ATTR_PARAMS_PROCESSED_ARRAY.  
  
 Antes de executar a declaração, o aplicativo define o valor de cada elemento de cada matriz vinculada. Quando a declaração é executada, o driver usa as informações armazenadas para recuperar os valores dos parâmetros e enviá-los para a fonte de dados; se possível, o driver deve enviar esses valores como matrizes. Embora o uso de matrizes de parâmetros seja melhor implementado executando a declaração SQL com todos os parâmetros da matriz com uma única chamada para a fonte de dados, esse recurso não está amplamente disponível em DBMSs hoje. No entanto, os drivers podem simular isso executando uma declaração SQL várias vezes, cada uma com um único conjunto de parâmetros.  
  
 Antes de um aplicativo usar matrizes de parâmetros, ele deve ter certeza de que eles são suportados pelos drivers usados pelo aplicativo. Há duas maneiras de fazer isso:  
  
-   Use apenas drivers conhecidos para suportar matrizes de parâmetros. O aplicativo pode codificar os nomes desses drivers, ou o usuário pode ser instruído a usar apenas esses drivers. Aplicativos personalizados e aplicativos verticais geralmente usam um conjunto limitado de drivers.  
  
-   Verifique se há suporte de matrizes de parâmetros no tempo de execução. Um driver suporta matrizes de parâmetros se for possível definir o atributo de declaração SQL_ATTR_PARAMSET_SIZE para um valor maior que 1. Aplicações genéricas e aplicações verticais geralmente verificam o suporte de matrizes de parâmetros em tempo de execução.  
  
 A disponibilidade de contagem de linhas e conjuntos de resultados em execução parametrizada pode ser determinada ligando para **SQLGetInfo** com as opções SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. Para **instruções INSERT**, **UPDATE**e **DELETE,** a opção SQL_PARAM_ARRAY_ROW_COUNTS indica se as contagens individuais de linha (uma para cada conjunto de parâmetros) estão disponíveis (SQL_PARC_BATCH) ou se as contagens de linha estão enroladas em uma (SQL_PARC_NO_BATCH). Para instruções **SELECT,** a opção SQL_PARAM_ARRAY_SELECTS indica se um conjunto de resultados está disponível para cada conjunto de parâmetros (SQL_PAS_BATCH) ou se apenas um conjunto de resultados está disponível (SQL_PAS_NO_BATCH). Se o driver não permitir que instruções de geração de resultados sejam executadas com uma matriz de parâmetros, SQL_PARAM_ARRAY_SELECTS retorna SQL_PAS_NO_SELECT. É específico da fonte de dados se os arrays de parâmetros podem ser usados com outros tipos de declarações, especialmente porque o uso de parâmetros nessas instruções seria específico para fonte de dados e não seguiria a gramática ODBC SQL.  
  
 O array apontado pelo atributo de declaração SQL_ATTR_PARAM_OPERATION_PTR pode ser usado para ignorar linhas de parâmetros. Se um elemento da matriz estiver definido como SQL_PARAM_IGNORE, o conjunto de parâmetros correspondentes a esse elemento será excluído da chamada **SQLExecute** ou **SQLExecDirect.** A matriz apontada pelo atributo SQL_ATTR_PARAM_OPERATION_PTR é alocada e preenchida pelo aplicativo e lida pelo driver. Se as linhas buscadas forem usadas como parâmetros de entrada, os valores da matriz de status da linha podem ser usados no conjunto de operação de parâmetros.  
  
## <a name="error-processing"></a>Processamento de erros  
 Se ocorrer um erro durante a execução da declaração, a função de execução retorna um erro e define a variável número de linha para o número da linha que contém o erro. É específico da fonte de dados se todas as linhas, exceto o conjunto de erros, forem executadas ou se todas as linhas antes (mas não depois) do conjunto de erros são executadas. Como processa conjuntos de parâmetros, o driver define o buffer especificado pelo SQL_ATTR_PARAMS_PROCESSED_PTR atributo de declaração ao número da linha atualmente em processo. Se todos os conjuntos, exceto o conjunto de erros forem executados, o driver definirá este buffer para SQL_ATTR_PARAMSET_SIZE depois que todas as linhas forem processadas.  
  
 Se o atributo de declaração SQL_ATTR_PARAM_STATUS_PTR tiver sido definido, **SQLExecute** ou **SQLExecDirect** retornarão o array de status do *parâmetro,* que fornece o status de cada conjunto de parâmetros. O conjunto de status do parâmetro é alocado pelo aplicativo e preenchido pelo driver. Seus elementos indicam se a declaração SQL foi executada com sucesso para a linha de parâmetros ou se ocorreu um erro durante o processamento do conjunto de parâmetros. Se ocorreu um erro, o driver define o valor correspondente na matriz de status do parâmetro para SQL_PARAM_ERROR e retorna SQL_SUCCESS_WITH_INFO. O aplicativo pode verificar a matriz de status para determinar quais linhas foram processadas. Usando o número da linha, o aplicativo pode muitas vezes corrigir o erro e retomar o processamento.  
  
 A forma como o array de status de parâmetro é usado é determinada pelo SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS opções retornadas por uma chamada para **SQLGetInfo**. Para **inserção,** **ATUALIZAÇÃO**e **DECLARAÇÕES DE EXCLUSão,** a matriz de status do parâmetro é preenchida com informações de status se SQL_PARC_BATCH for devolvida para SQL_PARAM_ARRAY_ROW_COUNTS, mas não se SQL_PARC_NO_BATCH for devolvida. Para instruções **SELECT,** a matriz de status do parâmetro é preenchida se SQL_PAS_BATCH for devolvida para SQL_PARAM_ARRAY_SELECT, mas não se SQL_PAS_NO_BATCH ou SQL_PAS_NO_SELECT for devolvida.  
  
## <a name="data-at-execution-parameters"></a>Parâmetros de dados em execução  
 Se algum dos valores no array comprimento/indicador for SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC *(comprimento),* os dados desses valores serão enviados com **SQLPutData** da maneira usual. Os seguintes aspectos deste processo têm comentários especiais porque não são facilmente óbvios:  
  
-   Quando o driver retorna SQL_NEED_DATA, ele deve definir o endereço da variável número de linha para a linha para a qual ele precisa de dados. Como no caso de valor único, o aplicativo não pode fazer quaisquer suposições sobre a ordem em que o motorista solicitará valores de parâmetro dentro de um único conjunto de parâmetros. Se ocorrer um erro na execução de um parâmetro de dados em execução, o buffer especificado pelo atributo de declaração SQL_ATTR_PARAMS_PROCESSED_PTR será definido para o número da linha em que ocorreu o erro, o status da linha na matriz de status da linha especificada pelo atributo de declaração SQL_ATTR_PARAM_STATUS_PTR é definido como SQL_PARAM_ERROR e a chamada para **SQLExecute,** **SQLDirectExec,** **SQLParamData**ou **SQLPutData** retorna SQL_ERROR. O conteúdo deste buffer é indefinido se **sqlexecute,** **SQLExecDirect**ou **SQLParamData** retornar SQL_STILL_EXECUTING.  
  
-   Como o driver não interpreta o valor no argumento *ParameterValuePtr* do **SQLBindParameter** para parâmetros de data-at-execution, se o aplicativo fornecer um ponteiro para uma matriz, **o SQLParamData** não extrai e retorna um elemento desta matriz para o aplicativo. Em vez disso, ele retorna o valor escalar que a aplicação havia fornecido. Isso significa que o valor retornado pelo **SQLParamData** não é suficiente para especificar o parâmetro para o qual o aplicativo precisa enviar dados; o aplicativo também precisa considerar o número da linha atual.  
  
     Quando apenas alguns dos elementos de um conjunto de parâmetros são parâmetros de data-at-execution, o aplicativo deve passar o endereço de uma matriz no *ParameterValuePtr* que contém elementos para todos os parâmetros. Este array é interpretado normalmente para os parâmetros que não são parâmetros de data-at-execution. Para os parâmetros de data-at-execution, o valor que o **SQLParamData** fornece ao aplicativo, que normalmente poderia ser usado para identificar os dados que o driver está solicitando nesta ocasião, é sempre o endereço do array.
