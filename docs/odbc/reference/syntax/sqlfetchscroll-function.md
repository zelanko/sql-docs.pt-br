---
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
ms.openlocfilehash: b6c65ef71f5c2cb9202ab788cac5e00357674f4a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285876"
---
# <a name="sqlfetchscroll-function"></a>Função SQLFetchScroll
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLFetchScroll** busca o conjunto de linhas especificada de dados do conjunto de resultados e retorna dados para todas as colunas vinculadas. Os conjuntos de linhas podem ser especificados em uma posição absoluta ou relativa ou por marcador.  
  
 Ao trabalhar com um driver ODBC 2.x, o Driver Manager mapeia essa função para **SQLExtendedFetch**. Para obter mais informações, consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *BuscarOrientação*  
 [Entrada]  
  
 Tipo de busca:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Para obter mais informações, consulte "Posicionando o Cursor" na seção "Comentários".  
  
 *FetchOffset*  
 [Entrada]  
  
 Número da fila para buscar. A interpretação deste argumento depende do valor do argumento *FetchOrientation.* Para obter mais informações, consulte "Posicionando o Cursor" na seção "Comentários".  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLFetchScroll** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um HandleType de SQL_HANDLE_STMT e uma alça de statementHandle. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLFetchScroll** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário. Se ocorrer um erro em uma única coluna, **o SQLGetDiagField** pode ser chamado com um DiagIdentifier de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que ocorreu o erro; e **SQLGetDiagField** pode ser chamado com um DiagIdentifier de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
 Para todos os SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO é devolvido se ocorrer um erro em uma ou mais linhas, mas não todas, linhas de uma operação multirow, e SQL_ERROR é devolvida se ocorrer um erro em uma operação de linha única.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Dados de seqüência ou binário retornados para uma coluna resultaram na truncação de caracteres não em branco ou dados binários não-NULOS. Se fosse um valor de corda, era truncado.|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas.<br /><br /> (Se este SQLSTATE for devolvido quando um aplicativo ODBC 3 *.x* estiver trabalhando com um driver ODBC*2.x,* ele pode ser ignorado.)|  
|01S06|Tentativa de buscar antes do conjunto de resultados retornou o primeiro conjunto de linhas|O conjunto de linhas solicitado sobrepôs-se ao início do conjunto de resultados quando fetchorientation foi SQL_FETCH_PRIOR, a posição atual estava além da primeira linha, e o número da linha atual é menor ou igual ao tamanho do conjunto de linhas.<br /><br /> O conjunto de linhas solicitado sobrepôs-se ao início do conjunto de resultados quando fetchorientation foi SQL_FETCH_PRIOR, a posição atual estava além do final do conjunto de resultados, e o tamanho do conjunto de linhas foi maior do que o tamanho do conjunto de resultados.<br /><br /> O conjunto de linhas solicitado se sobrepôs ao início do conjunto de resultados quando fetchorientation foi SQL_FETCH_RELATIVE, FetchOffset foi negativo, e o valor absoluto de FetchOffset foi menor ou igual ao tamanho do conjunto de linhas.<br /><br /> O conjunto de linhas solicitado sobrepôs-se ao início do conjunto de resultados quando fetchorientation foi SQL_FETCH_ABSOLUTE, FetchOffset foi negativo, e o valor absoluto de FetchOffset foi maior do que o tamanho do conjunto de resultados, mas menor ou igual ao tamanho do conjunto de linhas.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncação fracionada|Os dados devolvidos para uma coluna foram truncados. Para os tipos de dados numéricos, a parte fracionada do número foi truncada. Por tempo, carimbo de tempo e tipos de dados de intervalo contendo um componente de tempo, a parte fracionada do tempo foi truncada.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado pelo *TargetType* no **SQLBindCol**.<br /><br /> A coluna 0 estava vinculada a um tipo de SQL_C_BOOKMARK de dados, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE.<br /><br /> A coluna 0 estava vinculada a um tipo de SQL_C_VARBOOKMARK de dados, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS não foi definido como SQL_UB_VARIABLE.|  
|07009|Índice de descritor inválido|O driver era um driver ODBC*2.x* que não suporta **SQLExtendedFetch,** e um número de coluna especificado na vinculação para uma coluna era 0.<br /><br /> A coluna 0 estava vinculada, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22001|Dados de cordas, truncados direito|Um marcador de comprimento variável retornado para uma coluna foi truncado.|  
|22002|Variável indicador necessária, mas não fornecida|Os dados NULL foram obtidos em uma coluna cuja *StrLen_or_IndPtr* definida pelo **SQLBindCol** (ou SQL_DESC_INDICATOR_PTR definida por **SQLSetDescField** ou **SQLSetDescRec**) era um ponteiro nulo.|  
|22003|Valor numérico fora do alcance|Devolver o valor numérico (como numérico ou string) para uma ou mais colunas vinculadas teria feito com que a parte inteira (em oposição a fracionária) do número fosse truncada.<br /><br /> Para obter mais informações, [consulte Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no [Apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de data-hora inválido|Uma coluna de caracteres no conjunto de resultados estava vinculada a uma estrutura de data, hora ou carimbo de data C, e um valor na coluna era, respectivamente, uma data, hora ou carimbo de data inválidos.|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi devolvido, o que resultou em divisão por zero.|  
|22015|Estouro do campo de intervalo|Atribuir de um tipo sql numérico ou intervalado para um tipo de intervalo C causou uma perda de dígitos significativos no campo principal.<br /><br /> Ao buscar dados para um tipo C de intervalo, não houve representação do valor do tipo SQL no tipo C do intervalo.|  
|22018|Valor de caractere inválido para especificação do elenco|Uma coluna de caracteres no conjunto de resultados estava vinculada a um buffer de caractereC, e a coluna continha um caractere para o qual não havia representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna não era um literal válido do tipo C ligado.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|40001|Falha na serialização|A transação em que a busca foi executada foi encerrada para evitar impasse.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLFetchScroll** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) O *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem antes chamar **SQLExecDirect,** **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) **O SQLFetch** foi chamado para o *StatementHandle* depois que **o SQLExtendedFetch** foi chamado e antes **do SQLFreeStmt** com a opção SQL_CLOSE ser chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|O atributo de declaração SQL_ATTR_USE_BOOKMARK foi definido para SQL_UB_VARIABLE, e a coluna 0 estava vinculada a um buffer cujo comprimento não era igual ao comprimento máximo do marcador para este conjunto de resultados. (Este comprimento está disponível no campo SQL_DESC_OCTET_LENGTH do IRD e pode ser obtido ligando para **SQLDescribeCol,** **SQLColAttribute**ou **SQLGetDescField**.)|  
|HY106|Buscar tipo fora de alcance|DM) O valor especificado para o argumento FetchOrientation era inválido.<br /><br /> (DM) O argumento FetchOrientation foi SQL_FETCH_BOOKMARK, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF.<br /><br /> O valor do atributo de declaração SQL_ATTR_CURSOR_TYPE foi SQL_CURSOR_FORWARD_ONLY, e o valor do argumento FetchOrientation não foi SQL_FETCH_NEXT.<br /><br /> O valor do atributo de declaração SQL_ATTR_CURSOR_SCROLLABLE foi SQL_NONSCROLLABLE, e o valor do argumento FetchOrientation não foi SQL_FETCH_NEXT.|  
|HY107|Valor da linha fora do alcance|O valor especificado com o atributo de declaração SQL_ATTR_CURSOR_TYPE foi SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de declaração SQL_ATTR_KEYSET_SIZE foi maior que 0 e menor do que o valor especificado com o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE.|  
|HY111|Valor de marcador inválido|O argumento FetchOrientation foi SQL_FETCH_BOOKMARK, e o marcador apontado pelo valor no atributo de declaração SQL_ATTR_FETCH_BOOKMARK_PTR não era válido ou era um ponteiro nulo.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não suporta a conversão especificada pela combinação do *TargetType* no **SQLBindCol** e do tipo de dados SQL da coluna correspondente.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo é definido através de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLFetchScroll** retorna um conjunto de linhas especificado a partir do conjunto de resultados. Os conjuntos de linhas podem ser especificados por posição absoluta ou relativa ou por marcador. **SQLFetchScroll** só pode ser chamado enquanto existe um conjunto de resultados - ou seja, depois de uma chamada que cria um conjunto de resultados e antes que o cursor sobre esse conjunto de resultados seja fechado. Se alguma coluna estiver vinculada, ela retorna os dados nessas colunas. Se o aplicativo tiver especificado um ponteiro para uma matriz de status de linha ou um buffer no qual para retornar o número de linhas buscadas, **o SQLFetchScroll** também retorna essas informações. As chamadas para **SQLFetchScroll** podem ser misturadas com chamadas para **SQLFetch,** mas não podem ser misturadas com chamadas para **SQLExtendedFetch**.  
  
 Para obter mais informações, consulte [Usando cursors de bloco e](../../../odbc/reference/develop-app/using-block-cursors.md) usando [cursors roláveis](../../../odbc/reference/develop-app/using-scrollable-cursors.md).  
  
## <a name="positioning-the-cursor"></a>Posicionamento do Cursor  
 Quando o conjunto de resultados é criado, o cursor é posicionado antes do início do conjunto de resultados. **SQLFetchScroll** posiciona o cursor de bloco com base nos valores dos argumentos *FetchOrientation* e *FetchOffset,* conforme mostrado na tabela a seguir. As regras exatas para determinar o início do novo conjunto de linhas são mostradas na próxima seção.  
  
|BuscarOrientação|Significado|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Retorne o próximo conjunto de linhas. Isso equivale a chamar **SQLFetch**.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_PRIOR|Retorne o conjunto de linhas anterior.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Retorne o conjunto de linhas *FetchOffset* desde o início do conjunto de linhas atual.|  
|SQL_FETCH_ABSOLUTE|Retorne o conjunto de linhas a partir da linha *FetchOffset*.|  
|SQL_FETCH_FIRST|Retorne o primeiro conjunto de linhas no conjunto de resultados.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_LAST|Retorne a última linha completa definida no conjunto de resultados.<br /><br /> **SQLFetchScroll** ignora o valor de *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Retorne as linhas FetchOffset do marcador especificado pelo atributo de declaração SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
 Os motoristas não são obrigados a suportar todas as orientações de busca; um aplicativo chama **SQLGetInfo** com um tipo de informação de SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo do cursor) para determinar quais orientações de busca são suportadas pelo motorista. O aplicativo deve analisar os SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE e WQL_CA1_BOOKMARK máscaras de bits nesses tipos de informações. Além disso, se o cursor for apenas para a frente e o FetchOrientation não for SQL_FETCH_NEXT, **o SQLFetchScroll** retorna SQLSTATE HY106 (tipo buscar fora do alcance).  
  
 O atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE especifica o número de linhas no conjunto de linhas. Se o conjunto de linhas que está sendo buscado pelo **SQLFetchScroll** se sobrepor ao final do conjunto de resultados, **o SQLFetchScroll** reameda um conjunto de linhas parcial. Ou seja, se S + R - 1 for maior que L, onde S é a linha inicial do conjunto de linhas que está sendo buscada, R é o tamanho do conjunto de linhas, e L é a última linha no conjunto de resultados, então apenas as primeiras linhas L - S + 1 do conjunto de linhas são válidas. As demais linhas estão vazias e têm um status de SQL_ROW_NOROW.  
  
 Após o retorno **de SQLFetchScroll,** a linha atual é a primeira linha do conjunto de linhas.  
  
## <a name="cursor-positioning-rules"></a>Regras de posicionamento do cursor  
 As seções a seguir descrevem as regras exatas para cada valor de FetchOrientation. Essas regras usam a seguinte notação.  
  
|Notation|Significado|  
|--------------|-------------|  
|*Antes de começar*|O cursor de bloco é posicionado antes do início do conjunto de resultados. Se a primeira linha do novo conjunto de linhas for antes do início do conjunto de resultados, **SQLFetchScroll** retorna SQL_NO_DATA.|  
|*Depois do fim*|O cursor de bloco é posicionado após o término do conjunto de resultados. Se a primeira linha do novo conjunto de linhas estiver após o término do conjunto de resultados, **O SQLFetchScroll** retorna SQL_NO_DATA.|  
|*CurrRowsetStart*|O número da primeira linha no conjunto de linhas atual.|  
|*LastResultRow*|O número da última linha no conjunto de resultados.|  
|*Conjunto de linhasTamanho*|O tamanho do conjunto de linhas.|  
|*FetchOffset*|O valor do argumento *FetchOffset.*|  
|*BookmarkRow*|A linha correspondente ao marcador especificado pelo atributo de declaração SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 Aplicam-se as seguintes regras.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|*Antes de começar*|1|  
|*CurrRowsetStart + RowsetSize*[1] * \<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*Depois do fim*|  
|*Depois do fim*|*Depois do fim*|  
  
 [1] Se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, este é o tamanho do conjunto de linhas que foi usado com a chamada anterior.  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 Aplicam-se as seguintes regras.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|*Antes de começar*|*Antes de começar*|  
|*CurrRowsetStart = 1*|*Antes de começar*|  
|*1 < CurrRowsetStart <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > rowsetSize* <sup>[2]</sup>|*CurrRowsetStart - RowsetSize* <sup>[2]</sup>|  
|*Após o término e o último resultado, < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*Após o término e o último resultado >= RowsetSize* <sup>[2]</sup>|*LastResultRow - RowsetSize + 1* <sup>[2]</sup>|  
  
 [1] **SQLFetchScroll** retorna SQLSTATE 01S06 (Tentativa de buscar antes que o conjunto de resultados retorne o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [2] Se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, este é o novo tamanho do conjunto de linhas.  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 Aplicam-se as seguintes regras.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|*(Antes de iniciar e buscaroffset > 0) OU (Após o fim e fetchoffset < 0)*|*--*<sup>[1]</sup>|  
|*Antes de iniciar e buscar<= 0*|*Antes de começar*|  
|*CurrRowsetStart = 1 E FetchOffset < 0*|*Antes de começar*|  
|*CurrRowsetStart > 1 e CurrRowsetStart + FetchOffset < 1 e &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*Antes de começar*|  
|*CurrRowsetStart > 1 e CurrRowsetStart + FetchOffset < 1 E &#124; FetchOffset &#124; <= RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= CurrRowsetStart \<+ FetchOffset = LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*Depois do fim*|  
|*Após o término e fetchoffset >= 0*|*Depois do fim*|  
  
 [1] ***SQLFetchScroll*** retorna o mesmo conjunto de linhas como se fosse chamado com FetchOrientation definido para SQL_FETCH_ABSOLUTE. Para obter mais informações, consulte a seção "SQL_FETCH_ABSOLUTE".  
  
 [2] **SQLFetchScroll** retorna SQLSTATE 01S06 (Tentativa de buscar antes que o conjunto de resultados retorne o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [3] Se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, este é o novo tamanho do conjunto de linhas.  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 Aplicam-se as seguintes regras.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; <= LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; > LastResultRow e &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*Antes de começar*|  
|*FetchOffset < 0 E &#124; FetchOffset &#124; > LastResultRow E &#124; FetchOffset &#124; <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*Antes de começar*|  
|*1 <= \<FetchOffset = LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*Depois do fim*|  
  
 [1] **SQLFetchScroll** retorna SQLSTATE 01S06 (Tentativa de buscar antes que o conjunto de resultados retorne o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [2] Se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, este é o novo tamanho do conjunto de linhas.  
  
 Uma busca absoluta realizada contra um cursor dinâmico não pode fornecer o resultado necessário porque as posições de linha em um cursor dinâmico são indeterminadas. Tal operação é equivalente a uma busca primeiro seguido por um parente buscar; não é uma operação atômica, como é uma busca absoluta em um cursor estático.  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 Aplicam-se as seguintes regras.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|*Qualquer*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 Aplicam-se as seguintes regras.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> <= LastResultRow|*LastResultRow - RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] Se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, este é o novo tamanho de conjunto de linhas.  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 Aplicam-se as seguintes regras.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*Antes de começar*|  
|*1 <= BookmarkRow \<+ FetchOffset = LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*Depois do fim*|  
  
 Para obter informações sobre marcadores, consulte [Marcadores (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Efeito das linhas excluídas, adicionadas e de erro no movimento cursor  
 Cursores estáticos e orientados por chaves às vezes detectam linhas adicionadas ao conjunto de resultados e removem linhas excluídas do conjunto de resultados. Ao ligar para o **SQLGetInfo** com as opções de SQL_STATIC_CURSOR_ATTRIBUTES2 e SQL_KEYSET_CURSOR_ATTRIBUTES2 e olhar para as máscaras de bits SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS e SQL_CA2_SENSITIVITY_UPDATES, um aplicativo determina se os cursores implementados por um driver específico fazem isso. Para drivers que podem detectar linhas excluídas e removê-las, os seguintes parágrafos descrevem os efeitos desse comportamento. Para drivers que podem detectar linhas excluídas, mas não podem removê-las, as exclusões não têm efeito sobre os movimentos do cursor e os seguintes parágrafos não se aplicam.  
  
 Se o cursor detectar linhas adicionadas ao conjunto de resultados ou remover linhas excluídas do conjunto de resultados, ele aparecerá como se detectasse essas alterações somente quando buscasse dados. Isso inclui o caso em que o **SQLFetchScroll** é chamado com FetchOrientation definido para SQL_FETCH_RELATIVE e FetchOffset definido como 0 para rebuscar o mesmo conjunto de linhas, mas não inclui o caso quando SQLSetPos é chamado com fOption definido para SQL_REFRESH. Neste último caso, os dados nos buffers de conjunto de linhas são atualizados, mas não rebuscados, e as linhas excluídas não são removidas do conjunto de resultados. Assim, quando uma linha é excluída ou inserida no conjunto de linhas atual, o cursor não modifica os buffers do conjunto de linhas. Em vez disso, detecta a alteração quando busca qualquer conjunto de linhas que incluísse anteriormente a linha excluída ou agora inclua a linha inserida.  
  
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
  
 Quando **o SQLFetchScroll** retorna um novo conjunto de linhas que tem uma posição em relação ao conjunto de linhas atual - ou seja, FetchOrientation é SQL_FETCH_NEXT, SQL_FETCH_PRIOR ou SQL_FETCH_RELATIVE - ele não inclui alterações no conjunto de linhas atual ao calcular a posição inicial do novo conjunto de linhas. No entanto, ele inclui alterações fora do conjunto de linhas atual se for capaz de detectá-las. Além disso, quando **o SQLFetchScroll** retorna um novo conjunto de linhas que tem uma posição independente do conjunto de linhas atual - ou seja, FetchOrientation é SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE ou SQL_FETCH_BOOKMARK - ele inclui todas as alterações que é capaz de detectar, mesmo que estejam no conjunto de linhas atual.  
  
 Ao determinar se as linhas recém-adicionadas estão dentro ou fora do conjunto de linhas atual, considera-se que um conjunto de linhas parcial é considerado para terminar na última linha válida; ou seja, a última linha para a qual o status da linha não é SQL_ROW_NOROW. Por exemplo, suponha que o cursor seja capaz de detectar linhas recém-adicionadas, o conjunto de linhas atual é um conjunto de linhas parcial, o aplicativo adiciona novas linhas e o cursor adiciona essas linhas ao final do conjunto de resultados. Se o aplicativo chamar **SQLFetchScroll** com FetchOrientation definido para SQL_FETCH_NEXT, **O SQLFetchScroll** retorna o conjunto de linhas a partir da primeira linha recém-adicionada.  
  
 Por exemplo, suponha que o conjunto de linhas atual compreende as linhas 21 a 30, o tamanho do conjunto de linhas é 10, o cursor remove linhas excluídas do conjunto de resultados e o cursor detecta linhas adicionadas ao conjunto de resultados. A tabela a seguir mostra as linhas **que o SQLFetchScroll** retorna em várias situações.  
  
|Alterar|Tipo de busca|FetchOffset|Novo conjunto de linhas[1]|  
|------------|----------------|-----------------|---------------------|  
|Excluir a linha 21|NEXT|0|31 a 40|  
|Excluir linha 31|NEXT|0|32 a 41|  
|Inserir linha entre as linhas 21 e 22|NEXT|0|31 a 40|  
|Inserir linha entre as linhas 30 e 31|NEXT|0|Linha inserida, 31 a 39|  
|Excluir a linha 21|PRIOR|0|11 a 20|  
|Excluir linha 20|PRIOR|0|10 a 19|  
|Inserir linha entre as linhas 21 e 22|PRIOR|0|11 a 20|  
|Inserir linha entre as linhas 20 e 21|PRIOR|0|12 a 20, linha inserida|  
|Excluir a linha 21|RELATIVE|0|22 a 31<sup>[2]</sup>|  
|Excluir a linha 21|RELATIVE|1|22 a 31|  
|Inserir linha entre as linhas 21 e 22|RELATIVE|0|21, linha inserida, 22 a 29|  
|Inserir linha entre as linhas 21 e 22|RELATIVE|1|22 a 31|  
|Excluir a linha 21|ABSOLUTE|21|22 a 31<sup>[2]</sup>|  
|Excluir linha 22|ABSOLUTE|21|21, 23 a 31|  
|Inserir linha entre as linhas 21 e 22|ABSOLUTE|22|Linha inserida, 22 a 29|  
  
 [1] Esta coluna usa os números de linha antes de quaisquer linhas serem inseridas ou excluídas.  
  
 [2] Neste caso, o cursor tenta retornar linhas a partir da linha 21. Como a linha 21 foi excluída, a primeira linha que retorna é a linha 22.  
  
 As linhas de erro (ou seja, linhas com um status de SQL_ROW_ERROR) não afetam o movimento do cursor. Por exemplo, se o conjunto de linhas atual começar com a linha 11 e o status da linha 11 estiver SQL_ROW_ERROR, chamando **SQLFetchScroll** com FetchOrientation definido para SQL_FETCH_RELATIVE e FetchOffset definido para 5 retorna o conjunto de linhas começando pela linha 16, assim como seria se o status da linha 11 fosse SQL_SUCCESS.  
  
## <a name="returning-data-in-bound-columns"></a>Retornando dados em colunas vinculadas  
 **SQLFetchScroll** retorna dados em colunas vinculadas da mesma forma que **SQLFetch**. Para obter mais informações, consulte "Retornando dados em colunas vinculadas" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Se nenhuma coluna estiver vinculada, **o SQLFetchScroll** não retorna dados, mas move o cursor de bloco para a posição especificada. Se os dados podem ser recuperados a partir de colunas desvinculadas de um cursor de bloco com **SQLGetData** depende do driver. Esse recurso é suportado se uma chamada para **o SQLGetInfo** retornar o SQL_GD_BLOCK bit para o tipo de informação SQL_GETDATA_EXTENSIONS.  
  
## <a name="buffer-addresses"></a>Endereços de buffer  
 **SQLFetchScroll** usa a mesma fórmula para determinar o endereço dos buffers de dados e comprimento/indicador como **SQLFetch**. Para obter mais informações, consulte "Buffer Addresses" na [função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 **SQLFetchScroll** define valores na matriz de status da linha da mesma maneira que SQLFetch. Para obter mais informações, consulte "Row Status Array" na [função SQLFetch .](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
## <a name="rows-fetched-buffer"></a>Buffer de linhas buscadas  
 **SQLFetchScroll** retorna o número de linhas buscadas nas linhas buscadas buffer da mesma forma que **SQLFetch**. Para obter mais informações, consulte "Rows Fetched Buffer" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
 Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC 3.x, o Driver Manager chama **SQLFetchScroll** no driver. Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC 2.x, o Driver Manager chama SQLExtendedFetch no driver. Como **sQLFetchScroll** e SQLExtendedFetch lidam com erros de uma maneira ligeiramente diferente, o aplicativo vê um comportamento de erro ligeiramente diferente quando ele chama **SQLFetchScroll** em drivers ODBC 2.x e ODBC 3.x.  
  
 **SQLFetchScroll** retorna erros e avisos da mesma forma que **o SQLFetch;** para obter mais informações, consulte "Manipulação de erros" no **SQLFetch**. **SQLExtendedFetch** retorna erros da mesma forma que **SQLFetch,** com as seguintes exceções:  
  
 Quando ocorre um aviso que se aplica a uma linha específica no conjunto de linhas, sQLExtendedFetch define a entrada correspondente na matriz de status da linha para SQL_ROW_SUCCESS, não SQL_ROW_SUCCESS_WITH_INFO.  
  
 Se ocorrerem erros em todas as linhas do conjunto de linhas, o SQLExtendedFetch retorna SQL_SUCCESS_WITH_INFO, não SQL_ERROR.  
  
 Em cada grupo de registros de status que se aplica a uma linha individual, o primeiro registro de status retornado pelo SQLExtendedFetch deve conter SQLSTATE 01S01 (Erro em linha); **SQLFetchScroll** não retorna este SQLSTATE. Se o SQLExtendedFetch não puder retornar SQLSTATEs adicionais, ele ainda deve retornar este SQLSTATE.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll e Concorrência Otimista  
 Se um cursor usa uma concorrência otimista - ou seja, o atributo de declaração SQL_ATTR_CONCURRENCY tem um valor de SQL_CONCUR_VALUES ou SQL_CONCUR_ROWVER - o **SQLFetchScroll** atualiza os valores de concorrência otimistas usados pela fonte de dados para detectar se uma linha foi alterada. Isso acontece sempre que **o SQLFetchScroll** busca um novo conjunto de linhas, inclusive quando ele rebusca o conjunto de linhas atual. (É chamado com FetchOrientation definido para SQL_FETCH_RELATIVE e FetchOffset definido como 0.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>Drivers SQLFetchScroll e ODBC 2.x  
 Quando um aplicativo chama **SQLFetchScroll** em um driver ODBC 2.x, o Gerenciador de driver mapeia essa chamada para **SQLExtendedFetch**. Ele passa os seguintes valores para os argumentos de **SQLExtendedFetch**.  
  
|Argumento SQLExtendedFetch|Valor|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle em **SQLFetchScroll**.|  
|BuscarOrientação|FetchOrientation em **SQLFetchScroll**.|  
|FetchOffset|Se fetchOrientation não estiver SQL_FETCH_BOOKMARK, o valor do argumento FetchOffset no **SQLFetchScroll** será usado.<br /><br /> Se fetchorientation for SQL_FETCH_BOOKMARK, o valor armazenado no endereço especificado pelo atributo de declaração SQL_ATTR_FETCH_BOOKMARK_PTR é usado.|  
|RowCountPtr|O endereço especificado pelo atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR.|  
|LinhaStatusArray|O endereço especificado pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR.|  
  
 Para obter mais informações, consulte [Cursors de bloco, cursores roláveis e compatibilidade retrógrada](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Descritores e SQLFetchScroll  
 **SQLFetchScroll** interage com descritores da mesma forma que **SQLFetch**. Para obter mais informações, consulte a seção "Descritores e SQLFetchScroll" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [A vinculação em termos de coluna,](../../../odbc/reference/develop-app/column-wise-binding.md) [a vinculação em sentido de linha,](../../../odbc/reference/develop-app/row-wise-binding.md) [as instruções de atualização e exclusão posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)e [as linhas de atualização no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizando operações de inserção, atualização ou exclusão em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Fechando o cursor sobre a declaração|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Retornando o número de colunas de conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posicionando o cursor, atualizando dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
