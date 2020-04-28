---
title: Função SQLExtendedFetch | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc832e5a20b1d3c0a1ad63b3e2a070563de2b46d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285976"
---
# <a name="sqlextendedfetch-function"></a>Função SQLExtendedFetch
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: preterida  
  
 **Resumo**  
 **SQLExtendedFetch** busca o conjunto de linhas especificado de dados do conjunto de resultados e retorna dados para todas as colunas associadas. Os conjuntos de linhas podem ser especificados em uma posição absoluta ou relativa ou por indicador.  
  
> [!NOTE]
>  No ODBC 3 *. x*, **SQLExtendedFetch** foi substituído por **SQLFetchScroll**. Os aplicativos ODBC 3 *. x* não devem chamar **SQLExtendedFetch**; em vez disso, eles devem chamar **SQLFetchScroll**. O Gerenciador de driver mapeia **SQLFetchScroll** para **SQLExtendedFetch** ao trabalhar com um driver ODBC 2 *. x* . Os drivers ODBC 3 *. x* devem dar suporte a **SQLExtendedFetch** se desejarem trabalhar com aplicativos ODBC 2 *. x* que o chamam. Para obter mais informações, consulte "Comentários" e [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *FetchOrientation*  
 Entrada Tipo de busca. Isso é o mesmo que *FetchOrientation* em **SQLFetchScroll**.  
  
 *FetchOffset*  
 Entrada Número da linha a ser buscada. Isso é o mesmo que *FetchOffset* em **SQLFetchScroll**, com uma exceção. Quando *FetchOrientation* é SQL_FETCH_BOOKMARK, *FetchOffset* é um indicador de comprimento fixo, não um deslocamento de um indicador. Em outras palavras, **SQLExtendedFetch** recupera o indicador desse argumento, não o atributo de instrução SQL_ATTR_FETCH_BOOKMARK_PTR. Ele não dá suporte a indicadores de comprimento variável e não oferece suporte à busca de um conjunto de linhas em um deslocamento (diferente de 0) a partir de um indicador.  
  
 *RowCountPtr*  
 Der Ponteiro para um buffer no qual retornar o número de linhas realmente buscadas. Esse buffer é usado da mesma maneira que o buffer especificado pelo atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR. Esse buffer é usado somente por **SQLExtendedFetch**. Ele não é usado por **SQLFetch** ou **SQLFetchScroll**.  
  
 *RowStatusArray*  
 Der Ponteiro para uma matriz na qual retornar o status de cada linha. Essa matriz é usada da mesma maneira que a matriz especificada pelo atributo instrução SQL_ATTR_ROW_STATUS_PTR.  
  
 No entanto, o endereço dessa matriz não é armazenado no campo SQL_DESC_STATUS_ARRAY_PTR no IRD. Além disso, essa matriz é usada somente por **SQLExtendedFetch** e por **SQLBulkOperations** com uma *operação* de SQL_ADD ou **SQLSetPos** quando ela é chamada após **SQLExtendedFetch**. Ele não é usado por **SQLFetch** ou **SQLFetchScroll**e não é usado por **SQLBulkOperations** ou **SQLSetPos** quando eles são chamados após **SQLFetch** ou **SQLFetchScroll**. Ele também não é usado quando **SQLBulkOperations** com uma *operação* de SQL_ADD é chamado antes de qualquer função de busca ser chamada. Em outras palavras, ele é usado somente no estado de instrução S7. Ele não é usado nos Estados de instrução S5 ou s6. Para obter mais informações, consulte as [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: tabelas de transição de estado ODBC.  
  
 Os aplicativos devem fornecer um ponteiro válido no argumento *RowStatusArray* ; caso contrário, o comportamento de **SQLExtendedFetch** e o comportamento de chamadas para **SQLBulkOperations** ou **SQLSetPos** após um cursor ter sido posicionado por **SQLExtendedFetch** são indefinidos.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLExtendedFetch** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SqlError**. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLExtendedFetch** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário. Se ocorrer um erro em uma única coluna, **SQLGetDiagField** poderá ser chamado com um *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que o erro ocorreu; e **SQLGetDiagField** podem ser chamados com um *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Dados de cadeia de caracteres ou binários retornados para uma coluna resultaram no truncamento de um caractere não em branco ou dados binários não nulos. Se fosse um valor de cadeia de caracteres, ele foi truncado à direita. Se fosse um valor numérico, a parte fracionária do número foi truncada.  (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S06|Tentativa de busca antes de o conjunto de resultados retornar o primeiro conjunto de linhas|O conjunto de linhas solicitado se sobrepõe ao início do conjunto de resultados quando a posição atual estava além da primeira linha, e *FetchOrientation* era SQL_PRIOR ou *FetchOrientation* foi SQL_RELATIVE com um *FetchOffset* negativo cujo valor absoluto era menor ou igual ao SQL_ROWSET_SIZE atual. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamento fracionário|Os dados retornados para uma coluna foram truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para os tipos de dados time, timestamp e Interval que contêm um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|Um valor de dados não pôde ser convertido para o tipo de dados C especificado por *TargetType* em **SQLBindCol**.|  
|07009|Índice de descritor inválido|A coluna 0 foi associada a **SQLBindCol**e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22002|Variável de indicador necessária, mas não fornecida|Dados nulos foram buscados em uma coluna cujo *StrLen_or_IndPtr* definido por **SQLBindCol** era um ponteiro nulo.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|22003|Valor numérico fora do intervalo|Retornar o valor numérico (como numérico ou cadeia de caracteres) para uma ou mais colunas teria causado a parte inteira (em oposição à fração) do número a ser truncado.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obter mais informações, consulte [diretrizes para tipos de dados numéricos e de intervalo](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) no Apêndice D: tipos de dados.|  
|22007|Formato de data e hora inválido|Uma coluna de caracteres no conjunto de resultados foi associada a uma estrutura de data, hora ou carimbo de hora C e um valor na coluna era, respectivamente, uma data, hora ou carimbo de hora inválido.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi retornado, o que resultou em divisão por zero.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|22015|Estouro no campo de intervalo|A atribuição de um tipo de SQL numérico ou de intervalo exato para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao buscar dados para um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|22018|Valor de caractere inválido para especificação de conversão|O tipo C era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo associado de C.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SqlError** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado em *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLExtendedFetch** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) o *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute**ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) **SQLExtendedFetch** foi chamado para o *StatementHandle* após **SQLFetch** ou **SQLFetchScroll** ser chamado e antes de **SQLFreeStmt** ser chamado com a opção SQL_CLOSE.<br /><br /> (DM) **SQLBulkOperations** foi chamado para uma instrução antes de **SQLFetch**, **SQLFetchScroll**ou **SQLExtendedFetch** ser chamado e, em seguida, **SQLExtendedFetch** foi chamado antes de **SQLFreeStmt** ser chamado com a opção SQL_CLOSE.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY106|Tipo de busca fora do intervalo|(DM) o valor especificado para o argumento *FetchOrientation* era inválido. (Consulte "Comentários".)<br /><br /> O argumento *FetchOrientation* foi SQL_FETCH_BOOKMARK e o atributo SQL_ATTR_USE_BOOKMARKS Statement foi definido como SQL_UB_OFF.<br /><br /> O valor da opção de instrução SQL_CURSOR_TYPE foi SQL_CURSOR_FORWARD_ONLY e o valor do argumento *FetchOrientation* não foi SQL_FETCH_NEXT.<br /><br /> O argumento *FetchOrientation* foi SQL_FETCH_RESUME.|  
|HY107|Valor da linha fora do intervalo|O valor especificado com a opção de instrução SQL_CURSOR_TYPE foi SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de instrução SQL_KEYSET_SIZE era maior que 0 e menor que o valor especificado com o atributo de instrução SQL_ROWSET_SIZE.|  
|HY111|Valor de indicador inválido|O argumento *FetchOrientation* foi SQL_FETCH_BOOKMARK e o indicador especificado no argumento *FetchOffset* não era válido.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte ao tipo de busca especificado.<br /><br /> O driver ou a fonte de dados não oferece suporte à conversão especificada pela combinação de *TargetType* em **SQLBindCol** e o tipo de dados SQL da coluna correspondente. Esse erro se aplica somente quando o tipo de dados SQL da coluna foi mapeado para um tipo de dados SQL específico de driver.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 O comportamento de **SQLExtendedFetch** é idêntico ao de **SQLFetchScroll**, com as seguintes exceções:  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usam métodos diferentes para retornar o número de linhas buscadas. **SQLExtendedFetch** retorna o número de linhas buscadas em * \*RowCountPtr*; **SQLFetchScroll** retorna o número de linhas buscadas diretamente no buffer apontado por SQL_ATTR_ROWS_FETCHED_PTR. Para obter mais informações, consulte o argumento *RowCountPtr* .  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** retornam o status de cada linha em matrizes diferentes. Para obter mais informações, consulte o argumento *RowStatusArray* .  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usam métodos diferentes para recuperar o indicador quando *FetchOrientation* é SQL_FETCH_BOOKMARK. **SQLExtendedFetch** não dá suporte a indicadores de comprimento variável ou busca de conjuntos de linhas em um deslocamento diferente de 0 a partir de um indicador. Para obter mais informações, consulte o argumento *FetchOffset* .  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usam tamanhos de conjunto de linhas diferentes. **SQLExtendedFetch** usa o valor do atributo SQL_ROWSET_SIZE Statement e **SQLFetchScroll** usa o valor do atributo SQL_ATTR_ROW_ARRAY_SIZE Statement.  
  
-   **SQLExtendedFetch** tem uma semântica de tratamento de erros ligeiramente diferente da **SQLFetchScroll**. Para obter mais informações, consulte "tratamento de erro" na seção "Comentários" de [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** não dá suporte a deslocamentos de associação (o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   As chamadas para **SQLExtendedFetch** não podem ser misturadas com chamadas para **SQLFetch** ou **SQLFetchScroll**e, se **SQLBulkOperations** for chamado antes de qualquer função de busca ser chamada, **SQLExtendedFetch** não poderá ser chamado até que o cursor seja fechado e reaberto. Ou seja, **SQLExtendedFetch** pode ser chamado somente no estado da instrução S7. Para obter mais informações, consulte as [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: tabelas de transição de estado ODBC.  
  
 Quando um aplicativo chama **SQLFetchScroll** enquanto usa um driver ODBC 2 *. x* , o Gerenciador de driver mapeia essa chamada para **SQLExtendedFetch**. Para obter mais informações, consulte "drivers SQLFetchScroll e ODBC 2 *. x* " em [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 No ODBC 2 *. x*, **SQLExtendedFetch** foi chamado para buscar várias linhas e **SQLFetch** foi chamado para buscar uma única linha. No ODBC 3 *. x*, por outro lado, **SQLFetch** pode ser chamado para buscar várias linhas.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações de inserção, atualização ou exclusão em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o número de colunas do conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posicionando o cursor, atualizando os dados no conjunto de linhas, ou atualizando ou excluindo dados no grupo de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
