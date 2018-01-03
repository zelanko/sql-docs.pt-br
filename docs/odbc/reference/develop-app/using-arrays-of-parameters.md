---
title: "Usando matrizes de parâmetros | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da3d5662b8eb85f994142aea0e4dff237fd9852b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="using-arrays-of-parameters"></a>Usando matrizes de parâmetros
Para usar matrizes de parâmetros, o aplicativo chama **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_PARAMSET_SIZE para especificar o número de conjuntos de parâmetros. Ele chama **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_PARAMS_PROCESSED_PTR para especificar o endereço de uma variável na qual o driver pode retornar o número de conjuntos de parâmetros processados, incluindo conjuntos de erro. Ele chama **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_PARAM_STATUS_PTR para apontar para uma matriz no qual retornar informações de status para cada linha de valores de parâmetro. O driver armazena esses endereços na estrutura mantém para a instrução.  
  
> [!NOTE]  
>  No ODBC 2. *x*, **para SQLParamOptions** foi chamado para especificar vários valores para um parâmetro. Em ODBC 3. *x*, a chamada para **para SQLParamOptions** foi substituído por chamadas para **SQLSetStmtAttr** para definir os atributos SQL_ATTR_PARAMSET_SIZE e SQL_ATTR_PARAMS_PROCESSED_ARRAY .  
  
 Antes de executar a instrução, o aplicativo define o valor de cada elemento de cada matriz associada. Quando a instrução é executada, o driver usa as informações armazenada para recuperar os valores de parâmetro e enviá-los para a fonte de dados; Se possível, o driver deve enviar esses valores como matrizes. Embora o uso de matrizes de parâmetros é implementado da melhor forma, executando a instrução SQL com todos os parâmetros da matriz com uma única chamada para a fonte de dados, esse recurso não é amplamente disponível em DBMSs hoje. No entanto, drivers podem simular isso executando uma instrução SQL várias vezes, cada um com um único conjunto de parâmetros.  
  
 Para que um aplicativo usar matrizes de parâmetros, ele deve estar-se de que eles são suportados pelos drivers usados pelo aplicativo. Isso pode ser feito de duas maneiras:  
  
-   Use somente os drivers que sabem que oferecem suporte a matrizes de parâmetros. O aplicativo pode codificar os nomes desses drivers ou o usuário pode ser instruído a usar somente esses drivers. Aplicativos personalizados e aplicativos verticais geralmente usam um conjunto limitado de drivers.  
  
-   Verifique se há suporte a matrizes de parâmetros em tempo de execução. Um driver oferece suporte a matrizes de parâmetros, se é possível definir o atributo de instrução SQL_ATTR_PARAMSET_SIZE como um valor maior que 1. Aplicativos genéricos e aplicativos verticais geralmente Verifique para oferecer suporte a matrizes de parâmetros em tempo de execução.  
  
 A disponibilidade de contagens de linhas e conjuntos de resultados em execução com parâmetros pode ser determinada chamando **SQLGetInfo** com as opções SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. Para **inserir**, **atualização**, e **excluir** instruções, a opção SQL_PARAM_ARRAY_ROW_COUNTS indica se a contagem de linhas individuais (um para cada conjunto de parâmetros) disponível (SQL_PARC_BATCH) ou se contagens de linhas são acumuladas em um (SQL_PARC_NO_BATCH). Para **selecione** instruções, a opção SQL_PARAM_ARRAY_SELECTS indica se um conjunto de resultados está disponível para cada conjunto de parâmetros (SQL_PAS_BATCH) ou se apenas um conjunto de resultados está disponível (SQL_PAS_NO_BATCH). Se o driver não permitir que instruções de geração de conjunto de resultados a ser executado com uma matriz de parâmetros, SQL_PARAM_ARRAY_SELECTS retornará SQL_PAS_NO_SELECT. É específico da fonte de dados se matrizes de parâmetros podem ser usados com outros tipos de instruções, especialmente porque o uso de parâmetros nessas instruções seria específico de fonte de dados e não seria siga a gramática de SQL ODBC.  
  
 A matriz apontada pelo atributo SQL_ATTR_PARAM_OPERATION_PTR instrução pode ser usada para ignorar as linhas de parâmetros. Se um elemento da matriz é definido como SQL_PARAM_IGNORE, o conjunto de parâmetros correspondente a esse elemento é excluído do **SQLExecute** ou **SQLExecDirect** chamar. A matriz apontada pelo atributo SQL_ATTR_PARAM_OPERATION_PTR é alocada e preenchida pelo aplicativo e lido pelo driver. Se linhas buscadas são usadas como parâmetros de entrada, os valores da matriz de status de linha podem ser usados na matriz de operação de parâmetros.  
  
## <a name="error-processing"></a>Erro ao processar  
 Se ocorrer um erro ao executar a instrução, a função de execução retorna um erro e define a variável de número de linha com o número da linha que contém o erro. É específico da fonte de dados se todas as linhas, exceto o conjunto de erro são executados ou se todas as linhas antes (mas não depois) o conjunto de erro são executados. Como ele processa conjuntos de parâmetros, o driver define o buffer especificado pelo atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR para o número da linha que está sendo processado no momento. Se todos os conjuntos de exceto o conjunto de erro são executadas, o driver define esse buffer para SQL_ATTR_PARAMSET_SIZE depois que todas as linhas são processadas.  
  
 Se a instrução sql_attr_param_status_ptr tiver sido definida, **SQLExecute** ou **SQLExecDirect** retorna o *matriz de status de parâmetro,* que fornece o status cada conjunto de parâmetros. A matriz de status do parâmetro é alocada pelo aplicativo e preenchida pelo driver. Seus elementos indicam se a instrução SQL foi executada com êxito para a linha de parâmetros ou se ocorreu um erro ao processar o conjunto de parâmetros. Se ocorrer um erro, o driver define o valor correspondente na matriz de status de parâmetro para SQL_PARAM_ERROR e retornará SQL_SUCCESS_WITH_INFO. O aplicativo pode verificar se a matriz de status para determinar quais linhas foram processadas. Usando o número de linha, o aplicativo pode frequentemente corrija o erro e continuar o processamento.  
  
 Como a matriz de status do parâmetro é usada é determinada pelas opções de SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS retornadas por uma chamada para **SQLGetInfo**. Para **inserir**, **atualização**, e **excluir** declaração, a matriz de status do parâmetro é preenchido com as informações de status se SQL_PARC_BATCH for retornado para SQL_PARAM_ARRAY_ ROW_COUNTS, mas não se SQL_PARC_NO_BATCH é retornado. Para **selecione** instruções, a matriz de status de parâmetro é preenchida se SQL_PAS_BATCH é retornado para SQL_PARAM_ARRAY_SELECT, mas não se SQL_PAS_NO_BATCH ou SQL_PAS_NO_SELECT é retornado.  
  
## <a name="data-at-execution-parameters"></a>Parâmetros de dados em execução  
 Se qualquer um dos valores na matriz de comprimento/indicador são SQL_DATA_AT_EXEC ou o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro, os dados para os valores são enviados com **SQLPutData** como de costume. Os seguintes aspectos desse processo assume comentário especiais porque não são prontamente óbvios:  
  
-   Quando o driver retorna SQL_NEED_DATA, ele deve definir o endereço da variável de número de linha para a linha para que ele precisa de dados. Como no caso de valor único, o aplicativo não pode fazer suposições sobre a ordem na qual o driver solicitará valores de parâmetro em um único conjunto de parâmetros. Se ocorrer um erro na execução de um parâmetro de dados em execução, o buffer especificado pelo atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR é definido como o número da linha na qual o erro ocorreu, o status para a linha na matriz de status de linha especificada pelo a instrução sql_attr_param_status_ptr é definida como SQL_PARAM_ERROR e a chamada para **SQLExecute**, **SQLExecDirect**, **SQLParamData**, ou  **SQLPutData** retornará SQL_ERROR. O conteúdo desse buffer é indefinido se **SQLExecute**, **SQLExecDirect**, ou **SQLParamData** retornará SQL_STILL_EXECUTING.  
  
-   Porque o driver não interpreta o valor de *ParameterValuePtr* argumento de **SQLBindParameter** para parâmetros de dados em execução, se o aplicativo fornece um ponteiro para uma matriz,  **SQLParamData** não extrair e retornar um elemento dessa matriz para o aplicativo. Em vez disso, ele retorna que o valor escalar o aplicativo tinha fornecido. Isso significa que o valor retornado por **SQLParamData** é não é suficiente para especificar o parâmetro para o qual o aplicativo deve enviar dados; o aplicativo também deve considerar o número da linha atual.  
  
     Quando apenas alguns dos elementos de uma matriz de parâmetros são parâmetros de dados em execução, o aplicativo deve passar o endereço de uma matriz em *ParameterValuePtr* que contém elementos para todos os parâmetros. Esta matriz é interpretada normalmente para os parâmetros que não são parâmetros de dados em execução. Para os parâmetros de dados em execução, o valor que **SQLParamData** fornece para o aplicativo, que normalmente poderia ser usado para identificar os dados que o driver está solicitando esta vez, sempre é o endereço da matriz.
