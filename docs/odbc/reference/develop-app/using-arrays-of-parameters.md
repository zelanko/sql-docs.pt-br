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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306797"
---
# <a name="using-arrays-of-parameters"></a>Usar matrizes de parâmetros
Para usar matrizes de parâmetros, o aplicativo chama **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_PARAMSET_SIZE para especificar o número de conjuntos de parâmetros. Ele chama **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_PARAMS_PROCESSED_PTR para especificar o endereço de uma variável na qual o driver pode retornar o número de conjuntos de parâmetros processados, incluindo conjuntos de erros. Ele chama **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_PARAM_STATUS_PTR para apontar para uma matriz na qual retornar informações de status para cada linha de valores de parâmetro. O driver armazena esses endereços na estrutura que ele mantém para a instrução.  
  
> [!NOTE]  
>  No ODBC 2. *x*, **sqlparamoptions** foi chamado para especificar vários valores para um parâmetro. No ODBC 3. *x*, a chamada para **sqlparamoptions** foi substituída por chamadas para **SQLSetStmtAttr** para definir os atributos SQL_ATTR_PARAMSET_SIZE e SQL_ATTR_PARAMS_PROCESSED_ARRAY.  
  
 Antes de executar a instrução, o aplicativo define o valor de cada elemento de cada matriz associada. Quando a instrução é executada, o driver usa as informações que ele armazenou para recuperar os valores de parâmetro e enviá-los para a fonte de dados; se possível, o driver deve enviar esses valores como matrizes. Embora o uso de matrizes de parâmetros seja melhor implementado com a execução da instrução SQL com todos os parâmetros na matriz com uma única chamada para a fonte de dados, esse recurso não está amplamente disponível em DBMSs hoje. No entanto, os drivers podem simular isso executando uma instrução SQL várias vezes, cada um com um único conjunto de parâmetros.  
  
 Antes que um aplicativo use matrizes de parâmetros, ele deve ter a certeza de que eles têm suporte pelos drivers usados pelo aplicativo. Há duas maneiras de fazer isso:  
  
-   Use somente drivers conhecidos para dar suporte a matrizes de parâmetros. O aplicativo pode embutir os nomes desses drivers, ou o usuário pode ser instruído a usar apenas esses drivers. Aplicativos personalizados e aplicativos verticais normalmente usam um conjunto limitado de drivers.  
  
-   Verifique o suporte de matrizes de parâmetros em tempo de execução. Um driver oferece suporte a matrizes de parâmetros se for possível definir o atributo de instrução SQL_ATTR_PARAMSET_SIZE como um valor maior que 1. Aplicativos genéricos e verticais normalmente verificam o suporte de matrizes de parâmetros em tempo de execução.  
  
 A disponibilidade de contagens de linhas e conjuntos de resultados na execução parametrizada pode ser determinada chamando **SQLGetInfo** com as opções SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. Para instruções **Insert**, **Update**e **delete** , a opção SQL_PARAM_ARRAY_ROW_COUNTS indica se contagens de linhas individuais (uma para cada conjunto de parâmetros) estão disponíveis (SQL_PARC_BATCH) ou se as contagens de linhas são acumuladas em uma (SQL_PARC_NO_BATCH). Para instruções **Select** , a opção SQL_PARAM_ARRAY_SELECTS indica se um conjunto de resultados está disponível para cada conjunto de parâmetros (SQL_PAS_BATCH) ou se apenas um conjunto de resultados está disponível (SQL_PAS_NO_BATCH). Se o driver não permitir que instruções de geração de conjunto de resultados sejam executadas com uma matriz de parâmetros, SQL_PARAM_ARRAY_SELECTS retornará SQL_PAS_NO_SELECT. Ela é específica da fonte de dados se as matrizes de parâmetros podem ser usadas com outros tipos de instruções, especialmente porque o uso de parâmetros nessas instruções seria específico da fonte de dados e não segue a gramática do SQL do ODBC.  
  
 A matriz apontada pelo atributo instrução SQL_ATTR_PARAM_OPERATION_PTR pode ser usada para ignorar linhas de parâmetros. Se um elemento da matriz for definido como SQL_PARAM_IGNORE, o conjunto de parâmetros correspondente a esse elemento será excluído da chamada **SQLExecute** ou **SQLExecDirect** . A matriz apontada pelo atributo SQL_ATTR_PARAM_OPERATION_PTR é alocada e preenchida pelo aplicativo e lida pelo driver. Se as linhas buscadas forem usadas como parâmetros de entrada, os valores da matriz de status de linha poderão ser usados na matriz de operação de parâmetro.  
  
## <a name="error-processing"></a>Processamento de erro  
 Se ocorrer um erro durante a execução da instrução, a função de execução retornará um erro e definirá a variável de número de linha como o número da linha que contém o erro. É uma fonte de dados específica se todas as linhas, exceto o conjunto de erros, são executadas ou se todas as linhas antes (mas não depois) do conjunto de erros são executadas. Como ele processa conjuntos de parâmetros, o driver define o buffer especificado pelo atributo SQL_ATTR_PARAMS_PROCESSED_PTR Statement como o número da linha que está sendo processada no momento. Se todos os conjuntos, exceto o conjunto de erros, forem executados, o driver definirá esse buffer como SQL_ATTR_PARAMSET_SIZE depois que todas as linhas forem processadas.  
  
 Se o atributo de instrução SQL_ATTR_PARAM_STATUS_PTR tiver sido definido, **SQLExecute** ou **SQLExecDirect** retornará a matriz de *status de parâmetro,* que fornece o status de cada conjunto de parâmetros. A matriz de status de parâmetro é alocada pelo aplicativo e preenchida pelo driver. Seus elementos indicam se a instrução SQL foi executada com êxito para a linha de parâmetros ou se ocorreu um erro ao processar o conjunto de parâmetros. Se ocorreu um erro, o driver define o valor correspondente na matriz de status do parâmetro como SQL_PARAM_ERROR e retorna SQL_SUCCESS_WITH_INFO. O aplicativo pode verificar a matriz de status para determinar quais linhas foram processadas. Usando o número da linha, o aplicativo geralmente pode corrigir o erro e retomar o processamento.  
  
 Como a matriz de status de parâmetro é usada é determinada pelo SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS opções retornadas por uma chamada para **SQLGetInfo**. Para instruções **Insert**, **Update**e **delete** , a matriz de status de parâmetro é preenchida com informações de status se SQL_PARC_BATCH for retornado para SQL_PARAM_ARRAY_ROW_COUNTS, mas não se SQL_PARC_NO_BATCH for retornado. Para instruções **Select** , a matriz de status de parâmetro será preenchida se SQL_PAS_BATCH for retornada para SQL_PARAM_ARRAY_SELECT, mas não se SQL_PAS_NO_BATCH ou SQL_PAS_NO_SELECT for retornado.  
  
## <a name="data-at-execution-parameters"></a>Parâmetros de dados em execução  
 Se qualquer um dos valores na matriz de comprimento/indicador for SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*), os dados desses valores serão enviados com **SQLPutData** da maneira usual. Os seguintes aspectos desse processo têm um comentário especial, pois eles não são prontamente óbvios:  
  
-   Quando o driver retorna SQL_NEED_DATA, ele deve definir o endereço da variável de número de linha para a linha para a qual ela precisa de dados. Como no caso de valor único, o aplicativo não pode fazer suposições sobre a ordem em que o driver solicitará valores de parâmetro dentro de um único conjunto de parâmetros. Se ocorrer um erro na execução de um parâmetro de dados em execução, o buffer especificado pelo atributo instrução SQL_ATTR_PARAMS_PROCESSED_PTR será definido como o número da linha na qual o erro ocorreu, o status da linha na matriz de status de linha especificada pelo atributo instrução SQL_ATTR_PARAM_STATUS_PTR será definido como SQL_PARAM_ERROR e a chamada para **SQLExecute**, **SQLExecDirect**, **SQLParamData**ou **SQLPutData** retornará SQL_ERROR. O conteúdo desse buffer será indefinido se **SQLExecute**, **SQLExecDirect**ou **SQLParamData** retornará SQL_STILL_EXECUTING.  
  
-   Como o driver não interpreta o valor no argumento *ParameterValuePtr* de **SQLBindParameter** para parâmetros de dados em execução, se o aplicativo fornecer um ponteiro para uma matriz, **SQLParamData** não extrairá e retornará um elemento dessa matriz para o aplicativo. Em vez disso, ele retorna o valor escalar fornecido pelo aplicativo. Isso significa que o valor retornado por **SQLParamData** não é suficiente para especificar o parâmetro para o qual o aplicativo precisa enviar dados; o aplicativo também precisa considerar o número da linha atual.  
  
     Quando apenas alguns dos elementos de uma matriz de parâmetros são parâmetros de dados em execução, o aplicativo deve passar o endereço de uma matriz em *ParameterValuePtr* que contém elementos para todos os parâmetros. Essa matriz é interpretada normalmente para os parâmetros que não são parâmetros de dados em execução. Para os parâmetros de dados em execução, o valor que o **SQLParamData** fornece ao aplicativo, que normalmente poderia ser usado para identificar os dados que o driver está solicitando nessa ocasião, é sempre o endereço da matriz.
