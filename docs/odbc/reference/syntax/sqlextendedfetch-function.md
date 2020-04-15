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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285976"
---
# <a name="sqlextendedfetch-function"></a>Função SQLExtendedFetch
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: Preterido  
  
 **Resumo**  
 **SQLExtendedFetch** busca o conjunto de linhas especificada de dados do conjunto de resultados e retorna dados para todas as colunas vinculadas. Os conjuntos de linhas podem ser especificados em uma posição absoluta ou relativa ou por marcador.  
  
> [!NOTE]
>  Em ODBC 3 *.x,* **SQLExtendedFetch** foi substituído por **SQLFetchScroll**. Os aplicativos ODBC 3 *.x* não devem chamar **SQLExtendedFetch;** em vez disso, eles devem chamar **SQLFetchScroll**. O Driver Manager mapeia **SQLFetchScroll** para **SQLExtendedFetch** ao trabalhar com um driver ODBC*2.x.* Os drivers ODBC 3 *.x* devem suportar **o SQLExtendedFetch** se quiserem trabalhar com aplicativos ODBC 2 *.x* que o chamam. Para obter mais informações, consulte "Comentários" e [Cursores de Bloco, Cursores Roláveis e Compatibilidade Retrógrada](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no Apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
  
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
 [Entrada] Alça de declaração.  
  
 *BuscarOrientação*  
 [Entrada] Tipo de busca. Isso é o mesmo que *FetchOrientation* no **SQLFetchScroll**.  
  
 *FetchOffset*  
 [Entrada] Número da fila para buscar. Isso é o mesmo que *FetchOffset* no **SQLFetchScroll**, com uma exceção. Quando *fetchOrientation* é SQL_FETCH_BOOKMARK, *FetchOffset* é um marcador de comprimento fixo, não um deslocamento de um marcador. Em outras palavras, **SQLExtendedFetch** recupera o marcador deste argumento, não o atributo de declaração SQL_ATTR_FETCH_BOOKMARK_PTR. Ele não suporta marcadores de comprimento variável e não suporta buscar um conjunto de linhas em um offset (diferente de 0) de um marcador.  
  
 *RowCountPtr*  
 [Saída] Ponteiro para um buffer no qual para retornar o número de linhas realmente buscadas. Este buffer é usado da mesma forma que o buffer especificado pelo atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR. Este buffer é usado apenas por **SQLExtendedFetch**. Não é usado por **SQLFetch** ou **SQLFetchScroll**.  
  
 *LinhaStatusArray*  
 [Saída] Ponteiro para uma matriz na qual retornar o status de cada linha. Esta matriz é usada da mesma forma que a matriz especificada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR.  
  
 No entanto, o endereço desta matriz não é armazenado no campo SQL_DESC_STATUS_ARRAY_PTR no IRD. Além disso, este array é usado apenas por **SQLExtendedFetch** e por **SQLBulkOperations** com uma *operação* de SQL_ADD ou **SQLSetPos** quando é chamado após **SQLExtendedFetch**. Ele não é usado por **SQLFetch** ou **SQLFetchScroll**, e não é usado por **SQLBulkOperations** ou **SQLSetPos** quando eles são chamados após **SQLFetch** ou **SQLFetchScroll**. Ele também não é usado quando **SQLBulkOperations** com uma *Operação* de SQL_ADD é chamado antes de qualquer função de buscar é chamada. Em outras palavras, ele é usado apenas no estado de declaração S7. Não é usado nos estados de declaração S5 ou S6. Para obter mais informações, consulte [Transições de Declaração](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: Tabelas de transição do estado ODBC.  
  
 Os aplicativos devem fornecer um ponteiro válido no argumento *RowStatusArray;* se não, o comportamento do **SQLExtendedFetch** e o comportamento das chamadas para **SQLBulkOperations** ou **SQLSetPos** depois que um cursor foi posicionado pelo **SQLExtendedFetch** são indefinidos.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLExtendedFetch** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLError**. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLExtendedFetch** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário. Se ocorrer um erro em uma única coluna, **o SQLGetDiagField** pode ser chamado com um *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que ocorreu o erro; e **SQLGetDiagField** pode ser chamado com um *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Dados de seqüência ou binário retornados para uma coluna resultaram na truncação de caracteres não em branco ou dados binários não-NULOS. Se fosse um valor de corda, era truncado. Se fosse um valor numérico, a parte fracionada do número era truncada.  (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S06|Tentativa de buscar antes do conjunto de resultados retornou o primeiro conjunto de linhas|O conjunto de linhas solicitado sobrepôs-se ao início do conjunto de resultados quando a posição atual estava além da primeira linha, e ou *FetchOrientation* era SQL_PRIOR ou *FetchOrientation* era SQL_RELATIVE com um *FetchOffset* negativo cujo valor absoluto era menor ou igual ao SQL_ROWSET_SIZE atual. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncação fracionada|Os dados devolvidos para uma coluna foram truncados. Para os tipos de dados numéricos, a parte fracionada do número foi truncada. Por tempo, carimbo de tempo e tipos de dados de intervalo contendo um componente de tempo, a parte fracionada do tempo foi truncada.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|Um valor de dados não pôde ser convertido para o tipo de dados C especificado pelo *TargetType* no **SQLBindCol**.|  
|07009|Índice de descritor inválido|A coluna 0 estava ligada ao **SQLBindCol**, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22002|Variável indicador necessária, mas não fornecida|Os dados NULOS foram obtidos em uma coluna cujo *StrLen_or_IndPtr* definido pelo **SQLBindCol** era um ponteiro nulo.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|22003|Valor numérico fora do alcance|Devolver o valor numérico (como numérico ou string) para uma ou mais colunas teria feito com que a parte inteira (em oposição a fracionária) do número fosse truncada.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obter mais informações, consulte [Diretrizes para tipos de dados de intervalo e numéricos](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) no apêndice D: Tipos de dados.|  
|22007|Formato de data-hora inválido|Uma coluna de caracteres no conjunto de resultados estava vinculada a uma estrutura de data, hora ou carimbo de data C, e um valor na coluna era, respectivamente, uma data, hora ou carimbo de data inválidos.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi devolvido, o que resultou em divisão por zero.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|22015|Estouro do campo de intervalo|Atribuir de um tipo sql numérico ou intervalado para um tipo de intervalo C causou uma perda de dígitos significativos no campo principal.<br /><br /> Ao buscar dados para um tipo C de intervalo, não houve representação do valor do tipo SQL no tipo C do intervalo.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|22018|Valor de caractere inválido para especificação do elenco|O tipo C era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna não era um literal válido do tipo C ligado.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada por **SQLError** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLExtendedFetch** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) O *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem antes chamar **SQLExecDirect,** **SQLExecute**ou uma função de catálogo.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) **SQLExtendedFetch** foi chamado para o *StatementHandle* depois que **SQLFetch** ou **SQLFetchScroll** foi chamado e antes **de SQLFreeStmt** foi chamado com a opção SQL_CLOSE.<br /><br /> (DM) **A SQLBulkOperations** foi solicitada para uma declaração antes **de SQLFetch**, **SQLFetchScroll,** ou **SQLExtendedFetch** foi chamado, e então **SQLExtendedFetch** foi chamado antes **que SQLFreeStmt** fosse chamado com a opção SQL_CLOSE.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY106|Buscar tipo fora de alcance|(DM) O valor especificado para o argumento *FetchOrientation* era inválido. (Veja "Comentários".)<br /><br /> O argumento *FetchOrientation* foi SQL_FETCH_BOOKMARK, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF.<br /><br /> O valor da opção de declaração SQL_CURSOR_TYPE foi SQL_CURSOR_FORWARD_ONLY, e o valor do argumento *FetchOrientation* não foi SQL_FETCH_NEXT.<br /><br /> O argumento *FetchOrientation* foi SQL_FETCH_RESUME.|  
|HY107|Valor da linha fora do alcance|O valor especificado com a opção de declaração SQL_CURSOR_TYPE foi SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de declaração SQL_KEYSET_SIZE foi maior que 0 e menor do que o valor especificado com o atributo de declaração SQL_ROWSET_SIZE.|  
|HY111|Valor de marcador inválido|O argumento *FetchOrientation* foi SQL_FETCH_BOOKMARK, e o marcador especificado no argumento *FetchOffset* não era válido.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Driver ou fonte de dados não suporta o tipo de busca especificado.<br /><br /> O driver ou a fonte de dados não suporta a conversão especificada pela combinação do *TargetType* no **SQLBindCol** e do tipo de dados SQL da coluna correspondente. Esse erro só se aplica quando o tipo de dados SQL da coluna foi mapeado para um tipo de dados SQL específico do driver.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 O comportamento do **SQLExtendedFetch** é idêntico ao do **SQLFetchScroll,** com as seguintes exceções:  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usam diferentes métodos para retornar o número de linhas buscadas. **SQLExtendedFetch** retorna o número de linhas buscadas no * \*RowCountPtr*; **SQLFetchScroll** retorna o número de linhas buscadas diretamente para o buffer apontado por SQL_ATTR_ROWS_FETCHED_PTR. Para obter mais informações, consulte o argumento *RowCountPtr.*  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** retornam o status de cada linha em matrizes diferentes. Para obter mais informações, consulte o argumento *RowStatusArray.*  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usam métodos diferentes para recuperar o marcador quando *fetchorientation* é SQL_FETCH_BOOKMARK. **O SQLExtendedFetch** não suporta marcadores de comprimento variável ou conjuntos de linhas em um deslocamento diferente de 0 de um marcador. Para obter mais informações, consulte o argumento *FetchOffset.*  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usam diferentes tamanhos de conjunto de linhas. **O SQLExtendedFetch** usa o valor do atributo de declaração SQL_ROWSET_SIZE, e o **SQLFetchScroll** usa o valor do atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE.  
  
-   **SQLExtendedFetch** tem semântica de manipulação de erros ligeiramente diferente do **SQLFetchScroll**. Para obter mais informações, consulte "Manipulação de erros" na seção "Comentários" do [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **O SQLExtendedFetch** não suporta deslocamentos vinculativos (o atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   As chamadas para **SQLExtendedFetch** não podem ser misturadas com chamadas para **SQLFetch** ou **SQLFetchScroll,** e se **SQLBulkOperations** for chamado antes de qualquer função de buscar ser chamada, **o SQLExtendedFetch** não pode ser chamado até que o cursor seja fechado e reaberto. Ou seja, **SQLExtendedFetch** pode ser chamado apenas no estado de declaração S7. Para obter mais informações, consulte [Transições de Declaração](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: Tabelas de transição do estado ODBC.  
  
 Quando um aplicativo chama **SQLFetchScroll** ao usar um driver ODBC*2.x,* o Gerenciador de driver mapeia essa chamada para **SQLExtendedFetch**. Para obter mais informações, consulte "SQLFetchScroll e ODBC 2 *.x* Drivers" no [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 No ODBC*2.x,* **SQLExtendedFetch** foi chamado para buscar várias linhas e **SQLFetch** foi chamado para buscar uma única linha. Em ODBC 3 *.x*, por outro lado, **SQLFetch** pode ser chamado para buscar várias linhas.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizando operações de inserção, atualização ou exclusão em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o número de colunas de conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posicionando o cursor, atualizando dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
