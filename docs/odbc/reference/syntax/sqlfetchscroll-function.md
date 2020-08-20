---
description: Função SQLFetchScroll
title: Função SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e3c725e11c889765c18c2ff14625b6bde4705051
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476081"
---
# <a name="sqlfetchscroll-function"></a>Função SQLFetchScroll
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLFetchScroll** busca o conjunto de linhas especificado de dados do conjunto de resultados e retorna dados para todas as colunas associadas. Os conjuntos de linhas podem ser especificados em uma posição absoluta ou relativa ou por indicador.  
  
 Ao trabalhar com um driver ODBC 2. x, o Gerenciador de driver mapeia essa função para **SQLExtendedFetch**. Para obter mais informações, consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *FetchOrientation*  
 Entrada  
  
 Tipo de busca:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Para obter mais informações, consulte "posicionando o cursor" na seção "Comentários".  
  
 *FetchOffset*  
 Entrada  
  
 Número da linha a ser buscada. A interpretação desse argumento depende do valor do argumento *FetchOrientation* . Para obter mais informações, consulte "posicionando o cursor" na seção "Comentários".  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLFetchScroll** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um HandleType de SQL_HANDLE_STMT e um identificador de StatementHandle. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFetchScroll** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário. Se ocorrer um erro em uma única coluna, **SQLGetDiagField** poderá ser chamado com um DiagIdentifier de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que o erro ocorreu; e **SQLGetDiagField** podem ser chamados com um DiagIdentifier de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
 Para todos os sqlestaduais que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx sqlstates), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em uma ou mais, mas não em todas as linhas de uma operação multirow, e SQL_ERROR será retornado se ocorrer um erro em uma operação de linha única.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Dados de cadeia de caracteres ou binários retornados para uma coluna resultaram no truncamento de um caractere não em branco ou dados binários não nulos. Se fosse um valor de cadeia de caracteres, ele foi truncado à direita.|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas.<br /><br /> (Se esse SQLSTATE for retornado quando um aplicativo ODBC 3 *. x* estiver funcionando com um driver ODBC 2 *. x* , ele poderá ser ignorado.)|  
|01S06|Tentativa de busca antes de o conjunto de resultados retornar o primeiro conjunto de linhas|O conjunto de linhas solicitado se sobrepõe ao início do conjunto de resultados quando FetchOrientation foi SQL_FETCH_PRIOR, a posição atual estava além da primeira linha e o número da linha atual é menor ou igual ao tamanho do conjunto de linhas.<br /><br /> O conjunto de linhas solicitado se sobrepõe ao início do conjunto de resultados quando FetchOrientation foi SQL_FETCH_PRIOR, a posição atual estava além do fim do conjunto de resultados e o tamanho do conjunto de linhas era maior do que o tamanho do conjunto de resultados.<br /><br /> O conjunto de linhas solicitado se sobrepõe ao início do conjunto de resultados quando FetchOrientation foi SQL_FETCH_RELATIVE, FetchOffset era negativo, e o valor absoluto de FetchOffset era menor ou igual ao tamanho do conjunto de linhas.<br /><br /> O conjunto de linhas solicitado se sobrepõe ao início do conjunto de resultados quando FetchOrientation foi SQL_FETCH_ABSOLUTE, FetchOffset era negativo, e o valor absoluto de FetchOffset era maior que o tamanho do conjunto de resultados, mas menor ou igual ao tamanho de conjunto de linhas.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamento fracionário|Os dados retornados para uma coluna foram truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para os tipos de dados time, timestamp e Interval que contêm um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|Não foi possível converter o valor de dados de uma coluna no conjunto de resultados no tipo de dados especificado por *TargetType* em **SQLBindCol**.<br /><br /> A coluna 0 foi associada a um tipo de dados de SQL_C_BOOKMARK, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE.<br /><br /> A coluna 0 foi associada a um tipo de dados de SQL_C_VARBOOKMARK, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS não foi definido como SQL_UB_VARIABLE.|  
|07009|Índice de descritor inválido|O driver era um driver ODBC 2 *. x* que não oferece suporte a **SQLExtendedFetch**e um número de coluna especificado na associação para uma coluna era 0.<br /><br /> A coluna 0 foi associada e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22001|Dados de cadeia de caracteres, truncados à direita|Um indicador de comprimento variável retornado para uma coluna foi truncado.|  
|22002|Variável de indicador necessária, mas não fornecida|Dados nulos foram buscados em uma coluna cujo *StrLen_or_IndPtr* definido por **SQLBindCol** (ou SQL_DESC_INDICATOR_PTR definido por **SQLSetDescField** ou **SQLSetDescRec**) era um ponteiro nulo.|  
|22003|Valor numérico fora do intervalo|Retornar o valor numérico (como numérico ou cadeia de caracteres) para uma ou mais colunas associadas teria causado a parte inteira (em oposição à fracionária) do número a ser truncado.<br /><br /> Para obter mais informações, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de data e hora inválido|Uma coluna de caracteres no conjunto de resultados foi associada a uma estrutura de data, hora ou carimbo de hora C e um valor na coluna era, respectivamente, uma data, hora ou carimbo de hora inválido.|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi retornado, o que resultou em divisão por zero.|  
|22015|Estouro no campo de intervalo|A atribuição de um tipo de SQL numérico ou de intervalo exato para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao buscar dados para um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.|  
|22018|Valor de caractere inválido para especificação de conversão|Uma coluna de caracteres no conjunto de resultados foi associada a um buffer de caractere C e a coluna continha um caractere para o qual não havia nenhuma representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo associado de C.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|40001|Falha de serialização|A transação na qual a busca foi executada foi encerrada para evitar o deadlock.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLFetchScroll** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) o *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) **SQLFetch** foi chamado para *StatementHandle* depois que **SQLExtendedFetch** foi chamado e antes de **SQLFreeStmt** com a opção SQL_CLOSE foi chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|O atributo da instrução SQL_ATTR_USE_BOOKMARK foi definido como SQL_UB_VARIABLE e a coluna 0 foi associada a um buffer cujo comprimento não era igual ao tamanho máximo do indicador para esse conjunto de resultados. (Esse comprimento está disponível no campo SQL_DESC_OCTET_LENGTH do IRD e pode ser obtido chamando **SQLDescribeCol**, **SQLColAttribute**ou **SQLGetDescField**.)|  
|HY106|Tipo de busca fora do intervalo|DM) o valor especificado para o argumento FetchOrientation era inválido.<br /><br /> (DM) o argumento FetchOrientation foi SQL_FETCH_BOOKMARK e o atributo SQL_ATTR_USE_BOOKMARKS Statement foi definido como SQL_UB_OFF.<br /><br /> O valor do atributo da instrução SQL_ATTR_CURSOR_TYPE foi SQL_CURSOR_FORWARD_ONLY e o valor do argumento FetchOrientation não foi SQL_FETCH_NEXT.<br /><br /> O valor do atributo da instrução SQL_ATTR_CURSOR_SCROLLABLE foi SQL_NONSCROLLABLE e o valor do argumento FetchOrientation não foi SQL_FETCH_NEXT.|  
|HY107|Valor da linha fora do intervalo|O valor especificado com o atributo de instrução SQL_ATTR_CURSOR_TYPE foi SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de instrução SQL_ATTR_KEYSET_SIZE era maior que 0 e menor que o valor especificado com o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE.|  
|HY111|Valor de indicador inválido|O argumento FetchOrientation foi SQL_FETCH_BOOKMARK e o indicador apontado pelo valor no atributo da instrução SQL_ATTR_FETCH_BOOKMARK_PTR não era válido ou era um ponteiro nulo.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte à conversão especificada pela combinação de *TargetType* em **SQLBindCol** e o tipo de dados SQL da coluna correspondente.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo limite é definido por meio de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLFetchScroll** retorna um conjunto de linhas especificado do conjunto de resultados. Os conjuntos de linhas podem ser especificados por posição absoluta ou relativa ou por indicador. **SQLFetchScroll** pode ser chamado somente enquanto houver um conjunto de resultados – ou seja, após uma chamada que cria um conjunto de resultados e antes do cursor sobre esse conjunto de resultados ser fechado. Se alguma coluna estiver associada, ela retornará os dados nessas colunas. Se o aplicativo tiver especificado um ponteiro para uma matriz de status de linha ou um buffer no qual retornar o número de linhas buscadas, **SQLFetchScroll** retornará essas informações também. Chamadas para **SQLFetchScroll** podem ser misturadas com chamadas para **SQLFetch** , mas não podem ser misturadas com chamadas para **SQLExtendedFetch**.  
  
 Para obter mais informações, consulte [usando cursores de bloco](../../../odbc/reference/develop-app/using-block-cursors.md) e como [usar cursores roláveis](../../../odbc/reference/develop-app/using-scrollable-cursors.md).  
  
## <a name="positioning-the-cursor"></a>Posicionando o cursor  
 Quando o conjunto de resultados é criado, o cursor é posicionado antes do início do conjunto de resultados. **SQLFetchScroll** posiciona o cursor de bloco com base nos valores dos argumentos *FetchOrientation* e *FetchOffset* , conforme mostrado na tabela a seguir. As regras exatas para determinar o início do novo conjunto de linhas são mostradas na próxima seção.  
  
|FetchOrientation|Significado|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Retorna o próximo conjunto de linhas. Isso é equivalente a chamar **SQLFetch**.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_PRIOR|Retornar o conjunto de linhas anterior.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Retorne o conjunto de linhas *FetchOffset* do início do conjunto de linhas atual.|  
|SQL_FETCH_ABSOLUTE|Retornar o conjunto de linhas começando na linha *FetchOffset*.|  
|SQL_FETCH_FIRST|Retorna o primeiro conjunto de linhas no conjunto de resultados.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_LAST|Retorna o último conjunto de linhas completo no conjunto de resultados.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Retornar as linhas do conjunto de linhas FetchOffset do indicador especificado pelo atributo da instrução SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
 Não são necessários drivers para dar suporte a todas as orientações de busca; um aplicativo chama **SQLGetInfo** com um tipo de informação de SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo do cursor) para determinar quais orientações de busca são suportadas pelo driver. O aplicativo deve examinar as bitmasks SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE e WQL_CA1_BOOKMARK nesses tipos de informações. Além disso, se o cursor for somente encaminhamento e FetchOrientation não for SQL_FETCH_NEXT, **SQLFetchScroll** retornará SQLSTATE HY106 (tipo de busca fora do intervalo).  
  
 O atributo instrução SQL_ATTR_ROW_ARRAY_SIZE especifica o número de linhas no conjunto de linhas. Se o conjunto de linhas que está sendo buscado por **SQLFetchScroll** sobrepor o final do conjunto de resultados, **SQLFetchScroll** retornará um conjunto de linhas parcial. Ou seja, se S + R-1 for maior que L, onde S é a linha inicial do conjunto de linhas que está sendo obtido, R é o tamanho do conjunto de linhas e L é a última linha no conjunto de resultados, somente as primeiras L-S + 1 linhas do conjunto de linhas são válidas. As linhas restantes estão vazias e têm um status de SQL_ROW_NOROW.  
  
 Depois que **SQLFetchScroll** retorna, a linha atual é a primeira linha do conjunto de linhas.  
  
## <a name="cursor-positioning-rules"></a>Regras de posicionamento do cursor  
 As seções a seguir descrevem as regras exatas para cada valor de FetchOrientation. Essas regras usam a seguinte notação.  
  
|Notation|Significado|  
|--------------|-------------|  
|*Antes de iniciar*|O cursor de bloco está posicionado antes do início do conjunto de resultados. Se a primeira linha do novo conjunto de linhas for anterior ao início do conjunto de resultados, **SQLFetchScroll** retornará SQL_NO_DATA.|  
|*Após o término*|O cursor de bloco é posicionado após o final do conjunto de resultados. Se a primeira linha do novo conjunto de linhas for posterior ao final do conjunto de resultados, **SQLFetchScroll** retornará SQL_NO_DATA.|  
|*CurrRowsetStart*|O número da primeira linha no conjunto de linhas atual.|  
|*LastResultRow*|O número da última linha no conjunto de resultados.|  
|*Conjunto de linhas*|O tamanho do conjunto de linhas.|  
|*FetchOffset*|O valor do argumento *FetchOffset* .|  
|*BookmarkRow*|A linha correspondente ao indicador especificado pelo atributo da instrução SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 As regras a seguir se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*Antes de iniciar*|1|  
|*CurrRowsetStart + conjunto*de linhas [1] * \< = LastResultRow*|*CurrRowsetStart + conjunto*de linhas [1]|  
|*CurrRowsetStart + conjunto*[1]*> LastResultRow*|*Após o término*|  
|*Após o término*|*Após o término*|  
  
 [1] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, esse será o tamanho do conjunto de linhas usado com a chamada anterior.  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 As regras a seguir se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*Antes de iniciar*|*Antes de iniciar*|  
|*CurrRowsetStart = 1*|*Antes de iniciar*|  
|*1 < CurrRowsetStart <= conjunto* de linhas <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > conjunto* de linhas <sup>[2]</sup>|*CurrRowsetStart-conjunto de* linhas <sup>[2]</sup>|  
|*Após end e LastResultRow < o conjunto de* linhas <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*Após end e LastResultRow >= conjunto de* linhas <sup>[2]</sup>|*LastResultRow-conjunto de linhas + 1* <sup>[2]</sup>|  
  
 [1]   **SQLFetchScroll** retorna SQLSTATE 01S06 (tentativa de busca antes de o conjunto de resultados ter retornado o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [2] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, esse será o novo tamanho do conjunto de linhas.  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 As regras a seguir se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*(Antes de Start e FetchOffset > 0) OU (após end e FetchOffset < 0)*|*--*<sup>[1]</sup>|  
|*BeforeStart e FetchOffset <= 0*|*Antes de iniciar*|  
|*CurrRowsetStart = 1 e FetchOffset < 0*|*Antes de iniciar*|  
|*CurrRowsetStart > 1 e CurrRowsetStart + FetchOffset < 1 e &#124; FetchOffset &#124; > conjunto* de linhas <sup>[3]</sup>|*Antes de iniciar*|  
|*CurrRowsetStart > 1 e CurrRowsetStart + FetchOffset < 1 e &#124; FetchOffset &#124; <= conjunto* de linhas <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= CurrRowsetStart + FetchOffset \< = LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*Após o término*|  
|*Após end e FetchOffset >= 0*|*Após o término*|  
  
 [1]   ***SQLFetchScroll*** retorna o mesmo conjunto de linhas como se ele fosse chamado com FetchOrientation definido como SQL_FETCH_ABSOLUTE. Para obter mais informações, consulte a seção "SQL_FETCH_ABSOLUTE".  
  
 [2]   **SQLFetchScroll** retorna SQLSTATE 01S06 (tentativa de busca antes de o conjunto de resultados ter retornado o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [3] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, esse será o novo tamanho do conjunto de linhas.  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 As regras a seguir se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; <= LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; > LASTRESULTROW e &#124; FetchOffset &#124; > conjunto* de linhas <sup>[2]</sup>|*Antes de iniciar*|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; > LastResultRow e &#124; FetchOffset &#124; <= conjunto de* linhas <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*Antes de iniciar*|  
|*1 <= FetchOffset \< = LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*Após o término*|  
  
 [1]   **SQLFetchScroll** retorna SQLSTATE 01S06 (tentativa de busca antes de o conjunto de resultados ter retornado o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [2] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, esse será o novo tamanho do conjunto de linhas.  
  
 Uma busca absoluta executada em relação a um cursor dinâmico não pode fornecer o resultado necessário porque as posições de linha em um cursor dinâmico são indeterminadas. Essa operação é equivalente a uma busca primeiro seguida de uma busca relativa; Não é uma operação atômica, pois é uma busca absoluta em um cursor estático.  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 As regras a seguir se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*Qualquer*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 As regras a seguir se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*Conjunto* de linhas <sup>[1]</sup> <= LastResultRow|*LastResultRow-conjunto de linhas + 1* <sup>[1]</sup>|  
|*Conjunto* de linhas <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, esse será o novo tamanho do conjunto de linhas.  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 As regras a seguir se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*Antes de iniciar*|  
|*1 <= BookmarkRow + FetchOffset \< = LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*Após o término*|  
  
 Para obter informações sobre indicadores, consulte [indicadores (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Efeito de linhas excluídas, adicionadas e de erro no movimento do cursor  
 Os cursores estáticos e controlados por conjunto de chaves às vezes detectam linhas adicionadas ao conjunto de resultados e removem as linhas excluídas do conjunto de resultados. Chamando **SQLGetInfo** com as opções SQL_STATIC_CURSOR_ATTRIBUTES2 e SQL_KEYSET_CURSOR_ATTRIBUTES2 e examinando as bitmasks SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS e SQL_CA2_SENSITIVITY_UPDATES, um aplicativo determina se os cursores implementados por um determinado driver fazem isso. Para drivers que podem detectar linhas excluídas e removê-las, os parágrafos a seguir descrevem os efeitos desse comportamento. Para drivers que podem detectar linhas excluídas, mas não podem removê-las, as exclusões não têm nenhum efeito nos movimentos do cursor e os parágrafos a seguir não se aplicam.  
  
 Se o cursor detectar linhas adicionadas ao conjunto de resultados ou remover linhas excluídas do conjunto de resultados, ele aparecerá como se detectar essas alterações somente quando buscar dados. Isso inclui o caso em que **SQLFetchScroll** é chamado com FetchOrientation definido como SQL_FETCH_RELATIVE e FetchOffset definido como 0 para buscar novamente o mesmo conjunto de linhas, mas não inclui o caso quando SQLSetPos é chamado com fOption definido como SQL_REFRESH. No último caso, os dados nos buffers de conjunto de linhas são atualizados, mas não rebuscados, e as linhas excluídas não são removidas do conjunto de resultados. Assim, quando uma linha é excluída ou inserida no conjunto de linhas atual, o cursor não modifica os buffers de conjunto de linhas. Em vez disso, ele detecta a alteração quando busca qualquer conjunto de linhas que anteriormente incluía a linha excluída ou agora inclui a linha inserida.  
  
 Por exemplo:   
  
```cpp  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 Quando **SQLFetchScroll** retorna um novo conjunto de linhas que tem uma posição relativa ao conjunto de linhas atual, ou seja, FetchOrientation é SQL_FETCH_NEXT, SQL_FETCH_PRIOR ou SQL_FETCH_RELATIVE-ele não inclui alterações no conjunto de linhas atual ao calcular a posição inicial do novo conjunto de linhas. No entanto, ele inclui alterações fora do conjunto de linhas atual se for capaz de detectá-los. Além disso, quando **SQLFetchScroll** retorna um novo conjunto de linhas que tem uma posição independente do conjunto de linhas atual, ou seja, FetchOrientation é SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE ou SQL_FETCH_BOOKMARK-ele inclui todas as alterações que é capaz de detectar, mesmo se elas estiverem no conjunto de linhas atual.  
  
 Ao determinar se as linhas adicionadas recentemente estão dentro ou fora do conjunto de linhas atual, um conjunto de linhas parcial é considerado para terminar na última linha válida; ou seja, a última linha para a qual o status da linha não é SQL_ROW_NOROW. Por exemplo, suponha que o cursor seja capaz de detectar linhas adicionadas recentemente, o conjunto de linhas atual é um conjunto de linhas parcial, o aplicativo adiciona novas linhas e o cursor adiciona essas linhas ao final do conjunto de resultados. Se o aplicativo chamar **SQLFetchScroll** com FetchOrientation definido como SQL_FETCH_NEXT, **SQLFetchScroll** retornará o conjunto de linhas começando com a primeira linha recém-adicionada.  
  
 Por exemplo, suponha que o conjunto de linhas atual compreende as linhas 21 a 30, o tamanho do conjunto de linhas é 10, o cursor remove as linhas excluídas do conjunto de resultados e o cursor detecta as linhas adicionadas ao conjunto de resultados. A tabela a seguir mostra as linhas que o **SQLFetchScroll** retorna em várias situações.  
  
|Alterar|Tipo de busca|FetchOffset|Novo conjunto de linhas [1]|  
|------------|----------------|-----------------|---------------------|  
|Excluir linha 21|NEXT|0|31 a 40|  
|Excluir linha 31|NEXT|0|32 a 41|  
|Inserir linha entre as linhas 21 e 22|NEXT|0|31 a 40|  
|Inserir linha entre as linhas 30 e 31|NEXT|0|Linha inserida, 31 a 39|  
|Excluir linha 21|PRIOR|0|11 a 20|  
|Excluir linha 20|PRIOR|0|10 a 19|  
|Inserir linha entre as linhas 21 e 22|PRIOR|0|11 a 20|  
|Inserir linha entre as linhas 20 e 21|PRIOR|0|12 a 20, linha inserida|  
|Excluir linha 21|RELATIVE|0|22 a 31<sup>[2]</sup>|  
|Excluir linha 21|RELATIVE|1|22 a 31|  
|Inserir linha entre as linhas 21 e 22|RELATIVE|0|21, linha inserida, 22 a 29|  
|Inserir linha entre as linhas 21 e 22|RELATIVE|1|22 a 31|  
|Excluir linha 21|ABSOLUTE|21|22 a 31<sup>[2]</sup>|  
|Excluir linha 22|ABSOLUTE|21|21, 23 a 31|  
|Inserir linha entre as linhas 21 e 22|ABSOLUTE|22|Linha inserida, 22 a 29|  
  
 [1] esta coluna usa os números de linha antes que qualquer linha seja inserida ou excluída.  
  
 [2] nesse caso, o cursor tenta retornar linhas começando com a linha 21. Como a linha 21 foi excluída, a primeira linha retornada é a linha 22.  
  
 Linhas de erro (ou seja, linhas com um status de SQL_ROW_ERROR) não afetam o movimento do cursor. Por exemplo, se o conjunto de linhas atual começar com a linha 11 e o status da linha 11 for SQL_ROW_ERROR, chamar **SQLFetchScroll** com FetchOrientation definido como SQL_FETCH_RELATIVE e FetchOffset definido como 5 retornará o conjunto de linhas começando com a linha 16, exatamente como faria se o status da linha 11 fosse SQL_SUCCESS.  
  
## <a name="returning-data-in-bound-columns"></a>Retornando dados em colunas associadas  
 **SQLFetchScroll** retorna dados em colunas associadas da mesma maneira que **SQLFetch**. Para obter mais informações, consulte "retornando dados em colunas ligadas" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Se nenhuma coluna estiver associada, **SQLFetchScroll** não retornará dados, mas moverá o cursor de bloco para a posição especificada. Se os dados podem ser recuperados de colunas desassociadas de um cursor de bloco com **SQLGetData** depende do driver. Esse recurso terá suporte se uma chamada para **SQLGetInfo** retornar o bit SQL_GD_BLOCK para o tipo de informações SQL_GETDATA_EXTENSIONS.  
  
## <a name="buffer-addresses"></a>Endereços de buffer  
 **SQLFetchScroll** usa a mesma fórmula para determinar o endereço de dados e buffers de comprimento/indicador como **SQLFetch**. Para obter mais informações, consulte "endereços de buffer" na [função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 **SQLFetchScroll** define valores na matriz de status de linha da mesma maneira que SQLFetch. Para obter mais informações, consulte "matriz de status de linha" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="rows-fetched-buffer"></a>Buffers buscados de linhas  
 **SQLFetchScroll** retorna o número de linhas buscadas no buffer de linhas buscadas da mesma maneira que **SQLFetch**. Para obter mais informações, consulte "linhas buscadas no buffer" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
 Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC 3. x, o Gerenciador de driver chama **SQLFetchScroll** no driver. Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC 2. x, o Gerenciador de driver chama SQLExtendedFetch no driver. Como **SQLFetchScroll** e SQLExtendedFetch manipulam erros de maneira ligeiramente diferente, o aplicativo vê um comportamento de erro ligeiramente diferente quando chama **SQLFETCHSCROLL** nos drivers ODBC 2. x e ODBC 3. x.  
  
 **SQLFetchScroll** retorna erros e avisos da mesma maneira que **SQLFetch**; para obter mais informações, consulte "tratamento de erro" em **SQLFetch**. **SQLExtendedFetch** retorna erros da mesma maneira que **SQLFetch**, com as seguintes exceções:  
  
 Quando ocorre um aviso que se aplica a uma linha específica no conjunto de linhas, SQLExtendedFetch define a entrada correspondente na matriz de status de linha como SQL_ROW_SUCCESS, não SQL_ROW_SUCCESS_WITH_INFO.  
  
 Se ocorrerem erros em cada linha no conjunto de linhas, SQLExtendedFetch retornará SQL_SUCCESS_WITH_INFO, não SQL_ERROR.  
  
 Em cada grupo de registros de status que se aplica a uma linha individual, o primeiro registro de status retornado por SQLExtendedFetch deve conter SQLSTATE 01S01 (erro na linha); **SQLFetchScroll** não retorna este SQLSTATE. Se SQLExtendedFetch não puder retornar hiperestado adicional, ele ainda deverá retornar esse SQLSTATE.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll e simultaneidade otimista  
 Se um cursor usar simultaneidade otimista – ou seja, o atributo de instrução SQL_ATTR_CONCURRENCY terá um valor de SQL_CONCUR_VALUES ou SQL_CONCUR_ROWVER- **SQLFetchScroll** atualizará os valores de simultaneidade otimista usados pela fonte de dados para detectar se uma linha foi alterada. Isso acontece sempre que o **SQLFetchScroll** busca um novo conjunto de linhas, incluindo quando ele recupera o conjunto de linhas atual. (Ele é chamado com FetchOrientation definido como SQL_FETCH_RELATIVE e FetchOffset definido como 0.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>Drivers SQLFetchScroll e ODBC 2. x  
 Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC 2. x, o Gerenciador de driver mapeia essa chamada para **SQLExtendedFetch**. Ele passa os seguintes valores para os argumentos de **SQLExtendedFetch**.  
  
|Argumento SQLExtendedFetch|Valor|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle em **SQLFetchScroll**.|  
|FetchOrientation|FetchOrientation em **SQLFetchScroll**.|  
|FetchOffset|Se FetchOrientation não for SQL_FETCH_BOOKMARK, o valor do argumento FetchOffset em **SQLFetchScroll** será usado.<br /><br /> Se FetchOrientation for SQL_FETCH_BOOKMARK, o valor armazenado no endereço especificado pelo atributo instrução SQL_ATTR_FETCH_BOOKMARK_PTR será usado.|  
|RowCountPtr|O endereço especificado pelo atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR.|  
|RowStatusArray|O endereço especificado pelo atributo da instrução SQL_ATTR_ROW_STATUS_PTR.|  
  
 Para obter mais informações, consulte [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Descritores e SQLFetchScroll  
 O **SQLFetchScroll** interage com os descritores da mesma maneira que **SQLFetch**. Para obter mais informações, consulte a seção "descritores e SQLFetchScroll" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [Associação de coluna](../../../odbc/reference/develop-app/column-wise-binding.md), [Associação de linha](../../../odbc/reference/develop-app/row-wise-binding.md), instruções de [atualização e exclusão posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)e [atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações de inserção, atualização ou exclusão em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Fechando o cursor na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Retornando o número de colunas do conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posicionando o cursor, atualizando os dados no conjunto de linhas, ou atualizando ou excluindo dados no grupo de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
