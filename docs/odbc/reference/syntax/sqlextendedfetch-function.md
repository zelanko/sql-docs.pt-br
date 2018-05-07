---
title: Função SQLExtendedFetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a02b1c2e050b6fc7a0724286c7f023cb376e7bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlextendedfetch-function"></a>Função SQLExtendedFetch
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: Deprecated  
  
 **Resumo**  
 **SQLExtendedFetch** busca o conjunto de linhas especificado de dados do conjunto de resultados e retorna dados para todas as colunas associadas. Conjuntos de linhas podem ser especificados em uma posição absoluta ou relativa, ou pelo indicador.  
  
> [!NOTE]  
>  Em ODBC 3 *. x*, **SQLExtendedFetch** foi substituído pelo **SQLFetchScroll**. ODBC 3 *. x* aplicativos não devem chamar **SQLExtendedFetch**; em vez disso, eles devem chamar **SQLFetchScroll**. O Gerenciador de Driver mapeia **SQLFetchScroll** para **SQLExtendedFetch** ao trabalhar com um ODBC 2 *. x* driver. ODBC 3 *. x* devem dar suporte a drivers **SQLExtendedFetch** se desejar trabalhar com ODBC 2 *. x* aplicativos que chamá-lo. Para obter mais informações, consulte "Comentários" e [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *FetchOrientation*  
 [Entrada] Tipo de busca. Isso é o mesmo que *FetchOrientation* na **SQLFetchScroll**.  
  
 *FetchOffset*  
 [Entrada] Número da linha de busca. Isso é o mesmo que *FetchOffset* na **SQLFetchScroll**, com uma exceção. Quando *FetchOrientation* é SQL_FETCH_BOOKMARK, *FetchOffset* é um indicador de comprimento fixo, não um deslocamento de um indicador. Em outras palavras, **SQLExtendedFetch** recupera o indicador deste argumento, não o atributo da instrução SQL_ATTR_FETCH_BOOKMARK_PTR. Ele não oferece suporte a indicadores de comprimento variável e não dá suporte a busca de um conjunto de linhas em um deslocamento (diferente de 0) de um indicador.  
  
 *RowCountPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número de linhas buscadas realmente. Esse buffer é usado da mesma maneira como o buffer especificado pelo atributo SQL_ATTR_ROWS_FETCHED_PTR instrução. Esse buffer é usado apenas pelo **SQLExtendedFetch**. Não é usado por **SQLFetch** ou **SQLFetchScroll**.  
  
 *RowStatusArray*  
 [Saída] Ponteiro para uma matriz no qual retornar o status de cada linha. Esta matriz é usada da mesma maneira como a matriz especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.  
  
 No entanto, o endereço dessa matriz não é armazenado no campo SQL_DESC_STATUS_ARRAY_PTR do IRD. Além disso, esta matriz é usada apenas pelo **SQLExtendedFetch** e **SQLBulkOperations** com um *operação* de SQL_ADD ou **SQLSetPos**quando ele é chamado após **SQLExtendedFetch**. Não é usado por **SQLFetch** ou **SQLFetchScroll**, e ele não é usado por **SQLBulkOperations** ou **SQLSetPos** quando eles são chamados após **SQLFetch** ou **SQLFetchScroll**. Também não é usado quando **SQLBulkOperations** com um *operação* de SQL_ADD é chamado antes de qualquer função de busca é chamada. Em outras palavras, ele é usado apenas em estado de instrução S7. Ele não é usado nos Estados de instrução S5 ou S6. Para obter mais informações, consulte [instrução transições](../../../odbc/reference/appendixes/statement-transitions.md) nas tabelas de transição de estado do apêndice b: ODBC.  
  
 Aplicativos devem fornecer um ponteiro válido no *RowStatusArray* argumento; caso contrário, o comportamento de **SQLExtendedFetch** e o comportamento de chamadas para **SQLBulkOperations**ou **SQLSetPos** depois de um cursor tiver sido posicionado por **SQLExtendedFetch** são indefinidos.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLExtendedFetch** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLError**. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLExtendedFetch** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário. Se ocorrer um erro em uma única coluna, **SQLGetDiagField** pode ser chamado com um *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que o erro ocorreu em; e  **SQLGetDiagField** pode ser chamado com um *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Cadeia de caracteres ou dados binários retornados para uma coluna resultaram em truncamento de caracteres não vazia ou dados binários não nulo. Se fosse um valor de cadeia de caracteres, foi truncado à direita. Se fosse um valor numérico, a parte fracionária do número foi truncada.  (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S06|Tentativa de busca antes do conjunto de resultados retornado o primeiro conjunto de linhas|O conjunto de linhas solicitado overlapped o início do conjunto de resultados quando a posição atual foi além da primeira linha e ou *FetchOrientation* foi SQL_PRIOR ou *FetchOrientation* foi SQL_RELATIVE com um negativo *FetchOffset* cujo valor absoluto era menor ou igual ao SQL_ROWSET_SIZE atual. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamento fracionário|Os dados retornados de uma coluna foi truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para o tempo, carimbo de hora e tipos de dados de intervalo que contém um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|Um valor de dados não pôde ser convertido para o tipo de dados C especificado por *TargetType* na **SQLBindCol**.|  
|07009|Índice do descritor inválido|A coluna 0 foi associada com **SQLBindCol**, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22002|Variável de indicador exigida mas não fornecida|Dados nulos foi encontrados em uma coluna cujo *StrLen_or_IndPtr* definido por **SQLBindCol** foi um ponteiro nulo.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|22003|Valor numérico fora do intervalo|Retornando o valor numérico (como numérico ou cadeia de caracteres) para uma ou mais colunas causaria parte inteira (em vez de frações) o número a ser truncado.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obter mais informações, consulte [diretrizes para tipos de dados numéricos e de intervalo](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) no Apêndice d: os tipos de dados.|  
|22007|Formato de datetime inválido|Uma coluna de caractere no conjunto de resultados foi associada a uma data, hora ou estrutura de carimbo de hora C, e um valor na coluna foi, respectivamente, uma data inválida, hora ou carimbo de hora.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi retornado, resultando na divisão por zero.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|22015|Estouro no campo de intervalo|Atribuição de um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao buscar dados para um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|22018|Valor de caractere inválido para especificação de coerção|O tipo C foi um numérico exato ou aproximado, uma data e hora ou um tipo de dados do intervalo; o tipo SQL da coluna era de um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo C associado.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|24000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado a *StatementHandle*.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLError** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLExtendedFetch** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) especificado *StatementHandle* não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute**, ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) **SQLExtendedFetch** foi chamado para o *StatementHandle* depois **SQLFetch** ou **SQLFetchScroll** foi chamado e antes de  **SQLFreeStmt** foi chamado com a opção SQL_CLOSE.<br /><br /> (DM) **SQLBulkOperations** foi chamado para uma instrução antes de **SQLFetch**, **SQLFetchScroll**, ou **SQLExtendedFetch** foi chamado, e em seguida, **SQLExtendedFetch** foi chamado antes de **SQLFreeStmt** foi chamado com a opção SQL_CLOSE.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY106|Tipo de busca fora do intervalo|(DM) o valor especificado para o argumento *FetchOrientation* era inválido. (Consulte "Comentários".)<br /><br /> O argumento *FetchOrientation* foi SQL_FETCH_BOOKMARK, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF.<br /><br /> O valor da opção de instrução SQL_CURSOR_TYPE era SQL_CURSOR_FORWARD_ONLY e o valor do argumento *FetchOrientation* não era SQL_FETCH_NEXT.<br /><br /> O argumento *FetchOrientation* foi SQL_FETCH_RESUME.|  
|HY107|Valor de linha fora do intervalo|O valor especificado com a opção de instrução SQL_CURSOR_TYPE era SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de instrução SQL_KEYSET_SIZE era maior que 0 e menor que o valor especificado com o atributo de instrução SQL_ROWSET_SIZE .|  
|HY111|Valor inválido de indicador|O argumento *FetchOrientation* foi SQL_FETCH_BOOKMARK, e o indicador especificado no *FetchOffset* argumento não era válido.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Fonte de dados ou driver não oferece suporte para o tipo de busca especificado.<br /><br /> A driver ou fonte de dados não suporta a conversão especificada pela combinação da *TargetType* na **SQLBindCol** e o tipo de dados SQL da coluna correspondente. Esse erro se aplica somente quando o tipo de dados SQL da coluna foi mapeado para um tipo de dados SQL específico do driver.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 O comportamento de **SQLExtendedFetch** é idêntico de **SQLFetchScroll**, com as seguintes exceções:  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usar métodos diferentes para retornar o número de linhas buscadas. **SQLExtendedFetch** retorna o número de linhas buscadas no  *\*RowCountPtr*; **SQLFetchScroll** retorna o número de linhas buscadas diretamente para o buffer apontado pelo SQL_ATTR_ROWS_FETCHED_PTR. Para obter mais informações, consulte o *RowCountPtr* argumento.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** retorne o status de cada linha em diferentes matrizes. Para obter mais informações, consulte o *RowStatusArray* argumento.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usar métodos diferentes para recuperar o indicador quando *FetchOrientation* é SQL_FETCH_BOOKMARK. **SQLExtendedFetch** não oferece suporte a indicadores de comprimento variável ou conjuntos de linhas de buscando em um deslocamento diferente de 0 de um indicador. Para obter mais informações, consulte o *FetchOffset* argumento.  
  
-   **SQLExtendedFetch** e **SQLFetchScroll** usar tamanhos de conjunto de linhas diferentes. **SQLExtendedFetch** usa o valor do atributo de instrução SQL_ROWSET_SIZE e **SQLFetchScroll** usa o valor do atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE.  
  
-   **SQLExtendedFetch** tem semântica de tratamento de erros ligeiramente diferentes **SQLFetchScroll**. Para obter mais informações, consulte "Tratamento de erros" na seção "Comentários" [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** não oferece suporte para deslocamentos de associação (o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   Chamadas para **SQLExtendedFetch** não podem ser misturadas a chamadas para **SQLFetch** ou **SQLFetchScroll**e se **SQLBulkOperations** é chamado antes de qualquer função de busca é chamada, **SQLExtendedFetch** não pode ser chamado depois que o cursor for fechado e reaberto. Ou seja, **SQLExtendedFetch** pode ser chamado apenas em estado de instrução S7. Para obter mais informações, consulte [instrução transições](../../../odbc/reference/appendixes/statement-transitions.md) nas tabelas de transição de estado do apêndice b: ODBC.  
  
 Quando um aplicativo chama **SQLFetchScroll** ao usar um ODBC 2 *. x* driver, o Gerenciador de Driver mapeia essa chamada para **SQLExtendedFetch**. Para obter mais informações, consulte "SQLFetchScroll e ODBC 2 *. x* Drivers" em [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 No ODBC 2 *. x*, **SQLExtendedFetch** foi chamado para buscar várias linhas e **SQLFetch** foi chamado para buscar uma única linha. Em ODBC 3 *. x*, por outro lado, **SQLFetch** pode ser chamado para buscar várias linhas.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações de exclusão, atualização ou inserção em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Colunas do conjunto de retorno do número de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posicionando o cursor, atualizar dados no conjunto de linhas, ou atualizar ou excluir dados no conjunto de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
