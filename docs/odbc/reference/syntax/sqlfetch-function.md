---
title: Função SQLFetch | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e2da6996d8d6b2ee66befdc90794efec5617b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285966"
---
# <a name="sqlfetch-function"></a>Função SQLFetch
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLFetch** busca o próximo conjunto de dados do conjunto de resultados e retorna os dados de todas as colunas vinculadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLFetch** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para [a função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de handle of *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLFetch** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário. Se ocorrer um erro em uma única coluna, [o SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) pode ser chamado com um *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que ocorreu o erro; e **SQLGetDiagField** pode ser chamado com um *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
 Para todos os SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO é devolvido se ocorrer um erro em uma ou mais linhas, mas não todas, linhas de uma operação multirow, e SQL_ERROR é devolvida se ocorrer um erro em uma operação de linha única.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Dados de seqüência ou binário retornados para uma coluna resultaram na truncação de caracteres não em branco ou dados binários não-NULOS. Se fosse um valor de corda, era truncado.|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas.<br /><br /> (Se este SQLSTATE for devolvido quando um aplicativo ODBC 3 *.x* estiver trabalhando com um driver ODBC*2.x,* ele pode ser ignorado.)|  
|01S07|Truncação fracionada|Os dados devolvidos para uma coluna foram truncados. Para os tipos de dados numéricos, a parte fracionada do número foi truncada. Por tempo, data-hora e tipos de dados de intervalo que contêm um componente de tempo, a parte fracionada do tempo foi truncada.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado pelo *TargetType* no **SQLBindCol**.<br /><br /> A coluna 0 estava vinculada a um tipo de SQL_C_BOOKMARK de dados, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE.<br /><br /> A coluna 0 estava vinculada a um tipo de SQL_C_VARBOOKMARK de dados, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS não foi definido como SQL_UB_VARIABLE.|  
|07009|Índice de descritor inválido|O driver era um driver ODBC*2.x* que não suporta **SQLExtendedFetch,** e um número de coluna especificado na vinculação para uma coluna era 0.<br /><br /> A coluna 0 estava vinculada, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22001|Dados de cordas, truncados direito|Um marcador de comprimento variável retornado para uma coluna foi truncado.|  
|22002|Variável indicador necessária, mas não fornecida|Os dados NULL foram obtidos em uma coluna cuja *StrLen_or_IndPtr* definida pelo **SQLBindCol** (ou SQL_DESC_INDICATOR_PTR definida por **SQLSetDescField** ou **SQLSetDescRec**) era um ponteiro nulo.|  
|22003|Valor numérico fora do alcance|Devolver o valor numérico como numérico ou string para uma ou mais colunas vinculadas teria feito com que a parte inteira (em oposição a fracionária) do número fosse truncada.<br /><br /> Para obter mais informações, [consulte Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice D: Tipos de dados.|  
|22007|Formato de data-hora inválido|Uma coluna de caracteres no conjunto de resultados estava vinculada a uma estrutura de data, hora ou carimbo de data C, e um valor na coluna era, respectivamente, uma data, hora ou carimbo de data inválidos.|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi devolvido, o que resultou em divisão por zero.|  
|22015|Estouro do campo de intervalo|Atribuir de um tipo sql numérico ou intervalado para um tipo de intervalo C causou uma perda de dígitos significativos no campo principal.<br /><br /> Ao buscar dados para um tipo C de intervalo, não houve representação do valor do tipo SQL no tipo C do intervalo.|  
|22018|Valor de caractere inválido para especificação do elenco|Uma coluna de caracteres no conjunto de resultados estava vinculada a um buffer de caractereC, e a coluna continha um caractere para o qual não havia representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna não era um literal válido do tipo C ligado.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|40001|Falha na serialização|A transação em que a busca foi executada foi encerrada para evitar impasse.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função **SQLFetch** foi chamada e, antes de concluir a execução, **o SQLCancel** ou **o SQLCancelHandle** foram chamados no *StatementHandle*. Em seguida, a função **SQLFetch** foi chamada novamente no *StatementHandle*.<br /><br /> Ou, a função **SQLFetch** foi chamada e, antes de concluir a execução, **o SQLCancel** ou **o SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLFetch** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) O *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem antes chamar **SQLExecDirect,** **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) **O SQLFetch** foi chamado para o *StatementHandle* depois que **o SQLExtendedFetch** foi chamado e antes **do SQLFreeStmt** com a opção SQL_CLOSE ser chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|O atributo de declaração SQL_ATTR_USE_BOOKMARK foi definido para SQL_UB_VARIABLE, e a coluna 0 estava vinculada a um buffer cujo comprimento não era igual ao comprimento máximo do marcador para este conjunto de resultados. (Este comprimento está disponível no campo SQL_DESC_OCTET_LENGTH do IRD e pode ser obtido ligando para **SQLDescribeCol,** **SQLColAttribute**ou **SQLGetDescField**.)|  
|HY107|Valor da linha fora do alcance|O valor especificado com o atributo de declaração SQL_ATTR_CURSOR_TYPE foi SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de declaração SQL_ATTR_KEYSET_SIZE foi maior que 0 e menor do que o valor especificado com o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não suporta a conversão especificada pela combinação do *TargetType* no **SQLBindCol** e do tipo de dados SQL da coluna correspondente.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo é definido através de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLFetch** retorna o próximo conjunto de linhas no conjunto de resultados. Ele só pode ser chamado enquanto houver um conjunto de resultados: ou seja, depois de uma chamada que cria um conjunto de resultados e antes que o cursor sobre esse conjunto de resultados seja fechado. Se alguma coluna estiver vinculada, ela retorna os dados nessas colunas. Se o aplicativo tiver especificado um ponteiro para uma matriz de status de linha ou um buffer no qual para retornar o número de linhas buscadas, o **SQLFetch** também retorna essas informações. As chamadas para **SQLFetch** podem ser misturadas com chamadas para **SQLFetchScroll,** mas não podem ser misturadas com chamadas para **SQLExtendedFetch**. Para obter mais informações, consulte [Buscar uma linha de dados](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Se um aplicativo ODBC*3.x* funcionar com um driver ODBC*2.x,* o Driver Manager, o Driver Manager, derasno as chamadas **do SQLFetch** para **o SQLExtendedFetch** para um driver ODBC*2.x* que suporta **SQLExtendedFetch**. Se o driver ODBC*2.x* não suportar **sQLExtendedFetch,** o Driver Manager mapeia chamadas **sqlFetch** para **SQLFetch** no driver ODBC*2.x,* que pode buscar apenas uma linha.  
  
 Para obter mais informações, consulte [Cursors de bloco, cursores roláveis e compatibilidade retrógrada](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
  
## <a name="positioning-the-cursor"></a>Posicionamento do Cursor  
 Quando o conjunto de resultados é criado, o cursor é posicionado antes do início do conjunto de resultados. **SQLFetch** busca o próximo conjunto de linhas. Equivale a chamar **SQLFetchScroll** com *FetchOrientation* definido para SQL_FETCH_NEXT. Para obter mais informações sobre cursores, consulte [Cursors](../../../odbc/reference/develop-app/cursors.md) e [Cursors de Bloco .](../../../odbc/reference/develop-app/block-cursors.md)  
  
 O atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE especifica o número de linhas no conjunto de linhas. Se o conjunto de linhas que está sendo buscado pelo **SQLFetch** se sobrepor ao final do conjunto de resultados, o **SQLFetch** retorna um conjunto de linhas parcial. Ou seja, se S + R - 1 for maior que L, onde S é a linha inicial do conjunto de linhas que está sendo buscada, R é o tamanho do conjunto de linhas, e L é a última linha no conjunto de resultados, então apenas as primeiras linhas L - S + 1 do conjunto de linhas são válidas. As demais linhas estão vazias e têm um status de SQL_ROW_NOROW.  
  
 Após o retorno **do SQLFetch,** a linha atual é a primeira linha do conjunto de linhas.  
  
 As regras listadas na tabela a seguir descrevem o posicionamento do cursor após uma chamada ao **SQLFetch,** com base nas condições listadas na segunda tabela nesta seção.  
  
|Condição|Primeira linha de nova linha|  
|---------------|-----------------------------|  
|Antes de começar|1|  
|*CurrRowsetStart* \< =  *LastResultRow - RowsetSize*[1]|*CurrRowsetIniciar* + *conjunto de linhasTamanho*[2]|  
|*CurrRowsetStart* > *LastResultRow - RowsetSize*[1]|Depois do fim|  
|Depois do fim|Depois do fim|  
  
 [1] Se o tamanho do conjunto de linhas for alterado entre fetches, este é o tamanho do conjunto de linhas que foi usado com a busca anterior.  
  
 [2] Se o tamanho do conjunto de linhas for alterado entre fetches, este é o tamanho do conjunto de linhas que foi usado com a nova busca.  
  
|Notation|Significado|  
|--------------|-------------|  
|Antes de começar|O cursor de bloco é posicionado antes do início do conjunto de resultados. Se a primeira linha do novo conjunto de linhas for antes do início do conjunto de resultados, **o SQLFetch** retorna SQL_NO_DATA.|  
|Depois do fim|O cursor de bloco é posicionado após o término do conjunto de resultados. Se a primeira linha do novo conjunto de linhas for após o término do conjunto de resultados, o **SQLFetch** retorna SQL_NO_DATA.|  
|*CurrRowsetStart*|O número da primeira linha no conjunto de linhas atual.|  
|*LastResultRow*|O número da última linha no conjunto de resultados.|  
|*Conjunto de linhasTamanho*|O tamanho do conjunto de linhas.|  
  
 Por exemplo, suponha que um conjunto de resultados tenha 100 linhas e o tamanho do conjunto de linhas seja de 5. A tabela a seguir mostra o conjunto de linhas e o código de retorno retornado pelo **SQLFetch** para diferentes posições iniciais.  
  
|Conjunto de linhas atual|Código de retorno|Novo conjunto de linhas|# de linhas buscadas|  
|--------------------|-----------------|----------------|------------------------|  
|Antes de começar|SQL_SUCCESS|De 1 a 5|5|  
|De 1 a 5|SQL_SUCCESS|6 a 10|5|  
|52 a 56|SQL_SUCCESS|57 a 61|5|  
|91 a 95|SQL_SUCCESS|96 a 100|5|  
|93 a 97|SQL_SUCCESS|98 a 100. As linhas 4 e 5 da matriz de status da linha estão definidas para SQL_ROW_NOROW.|3|  
|96 a 100|SQL_NO_DATA|Nenhum.|0|  
|99 a 100|SQL_NO_DATA|Nenhum.|0|  
|Depois do fim|SQL_NO_DATA|Nenhum.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Retornando dados em colunas vinculadas  
 À medida que **o SQLFetch** retorna cada linha, ele coloca os dados de cada coluna vinculada no buffer vinculado a essa coluna. Se nenhuma coluna estiver vinculada, **o SQLFetch** não retorna dados, mas move o cursor de bloco para a frente. Os dados ainda podem ser recuperados usando **SQLGetData**. Se o cursor for um cursor multirow (ou seja, o SQL_ATTR_ROW_ARRAY_SIZE for maior que 1), **o SQLGetData** só poderá ser chamado se SQL_GD_BLOCK for devolvido quando **o SQLGetInfo** for chamado com um *InfoType* de SQL_GETDATA_EXTENSIONS. (Para obter mais informações, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Para cada coluna vinculada em uma linha, **o SQLFetch** faz o seguinte:  
  
1.  Define o buffer de comprimento/indicador para SQL_NULL_DATA e prossegue para a próxima coluna se os dados forem NULOS. Se os dados forem NULOS e nenhum buffer de comprimento/indicador estiver vinculado, **o SQLFetch** retorna SQLSTATE 22002 (variável indicador necessária, mas não fornecida) para a linha e segue para a próxima linha. Para obter informações sobre como determinar o endereço do buffer de comprimento/indicador, consulte "Buffer Addresses" no [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Se os dados da coluna não forem NULOS, **o SQLFetch** prosseguirá para a etapa 2.  
  
2.  Se o atributo de declaração SQL_ATTR_MAX_LENGTH for definido como um valor não zero e a coluna contiver caracteres ou dados binários, os dados são truncados para SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  O atributo de declaração SQL_ATTR_MAX_LENGTH destina-se a reduzir o tráfego da rede. Geralmente é implementado pela fonte de dados, que trunca os dados antes de devolvê-los pela rede. Drivers e fontes de dados não são necessários para apoiá-lo. Portanto, para garantir que os dados sejam truncados para um determinado tamanho, um aplicativo deve alocar um buffer desse tamanho e especificar o tamanho no argumento *cbValueMax* no **SQLBindCol**.  
  
3.  Converte os dados para o tipo especificado pelo *TargetType* no **SQLBindCol**.  
  
4.  Se os dados foram convertidos em um tipo de dados de comprimento variável, como caractere ou binário, o **SQLFetch** verifica se o comprimento dos dados excede o comprimento do buffer de dados. Se o comprimento dos dados de caracteres (incluindo o caractere de rescisão nula) exceder o comprimento do buffer de dados, o **SQLFetch** truncará os dados para o comprimento do buffer de dados menos o comprimento de um caractere de rescisão nula. Em seguida, anula os dados. Se o comprimento dos dados binários exceder o comprimento do buffer de dados, o **SQLFetch** truncará-o até o comprimento do buffer de dados. O comprimento do buffer de dados é especificado com *BufferLength* no **SQLBindCol**.  
  
     **O SQLFetch** nunca trunca dados convertidos em tipos de dados de comprimento fixo; ele sempre assume que o comprimento do buffer de dados é o tamanho do tipo de dados.  
  
5.  Coloca os dados convertidos (e possivelmente truncados) no buffer de dados. Para obter informações sobre como determinar o endereço do buffer de dados, consulte "Buffer Addresses" no [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  Coloca o comprimento dos dados no buffer de comprimento/indicador. Se o ponteiro indicador e o ponteiro de comprimento foram definidos para o mesmo buffer (como uma chamada para **SQLBindCol** faz), o comprimento é gravado no buffer para dados válidos e SQL_NULL_DATA é gravado no buffer para dados NULL. Se nenhum buffer de comprimento/indicador foi vinculado, **o SQLFetch** não retorna o comprimento.  
  
    -   Para dados de caracteres ou binários, este é o comprimento dos dados após a conversão e antes da truncação por causa do buffer de dados ser muito pequeno. Se o driver não puder determinar o comprimento dos dados após a conversão, como às vezes é o caso com dados longos, ele define o comprimento para SQL_NO_TOTAL. Se os dados foram truncados por causa do atributo de declaração SQL_ATTR_MAX_LENGTH, o valor deste atributo é colocado no buffer comprimento/indicador em vez do comprimento real . Isso porque este atributo foi projetado para truncar dados no servidor antes da conversão, de modo que o driver não tem como descobrir qual é o comprimento real.  
  
    -   Para todos os outros tipos de dados, este é o comprimento dos dados após a conversão; ou seja, é o tamanho do tipo para o qual os dados foram convertidos.  
  
     Para obter informações sobre como determinar o endereço do buffer de comprimento/indicador, consulte "Buffer Addresses" no [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Se os dados forem truncados durante a conversão sem perda de dígitos significativos (por exemplo, o número real 1.234 é truncado para o inteiro 1 quando convertido), **o SQLFetch** retorna SQLSTATE 01S07 (truncação fracionada) e SQL_SUCCESS_WITH_INFO. Se os dados forem truncados porque o comprimento do buffer de dados for muito pequeno (por exemplo, a string "abcdef" for colocada em um buffer de 4 bytes), **o SQLFetch** retorna SQLSTATE 01004 (Dados truncados) e SQL_SUCCESS_WITH_INFO. Se os dados forem truncados por causa do atributo de declaração SQL_ATTR_MAX_LENGTH, o **SQLFetch** retorna SQL_SUCCESS e não retorna SQLSTATE 01S07 (truncação fracionada) ou SQLSTATE 01004 (Dados truncados). Se os dados forem truncados durante a conversão com uma perda de dígitos significativos (por exemplo, se um valor SQL_INTEGER maior que 100.000 for convertido para um SQL_C_TINYINT), **o SQLFetch** retorna SQLSTATE 22003 (valor numérico fora do alcance) e SQL_ERROR (se o tamanho do rowset for 1) ou SQL_SUCCESS_WITH_INFO (se o tamanho do rowset for maior que 1).  
  
 O conteúdo do buffer de dados vinculado e do buffer de comprimento/indicador são indefinidos se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 A matriz de status da linha é usada para retornar o status de cada linha no conjunto de linhas. O endereço desta matriz é especificado com o atributo de declaração SQL_ATTR_ROW_STATUS_PTR. O array é alocado pelo aplicativo e deve ter tantos elementos quanto são especificados pelo atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE. Seus valores são definidos por **SQLFetch,** **SQLFetchScroll**e **SQLBulkOperations** ou **SQLSetPos** (exceto quando eles foram chamados após o cursor ter sido posicionado por **SQLExtendedFetch**). Se o valor do atributo de declaração SQL_ATTR_ROW_STATUS_PTR for um ponteiro nulo, essas funções não retornarão o status da linha.  
  
 O conteúdo do buffer de array de status da linha é indefinido se **sqlfetch** ou **SQLFetchScroll** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
 Os valores a seguir são retornados na matriz de status da linha.  
  
|Valor da matriz de status da linha|Descrição|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A linha foi buscada com sucesso e não mudou desde a última vez que foi buscada a partir deste conjunto de resultados.|  
|SQL_ROW_SUCCESS_WITH_INFO|A linha foi buscada com sucesso e não mudou desde a última vez que foi buscada a partir deste conjunto de resultados. No entanto, um aviso foi devolvido sobre a linha.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED[1],[2], e [3]|A linha foi buscada com sucesso e mudou desde a última vez que foi buscada a partir deste conjunto de resultados. Se a linha for retomada a partir deste conjunto de resultados ou for atualizada por **SQLSetPos,** o status será alterado para o novo status da linha.|  
|SQL_ROW_DELETED[3]|A linha foi excluída desde a última vez que foi retirada deste conjunto de resultados.|  
|SQL_ROW_ADDED[4]|A linha foi inserida pela **SQLBulkOperations**. Se a linha for retomada a partir deste conjunto de resultados ou for atualizada por **SQLSetPos,** seu status será SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|O conjunto de linhas sobrepôs-se ao final do conjunto de resultados, e nenhuma linha foi devolvida que correspondia a este elemento da matriz de status da linha.|  
  
 [1] Para os cursores de conjunto de chaves, mistos e dinâmicos, se um valor-chave for atualizado, a linha de dados é considerada excluída e uma nova linha adicionada.  
  
 [2] Alguns drivers não podem detectar atualizações de dados e, portanto, não podem retornar esse valor. Para determinar se um driver pode detectar atualizações em linhas rebuscadas, um aplicativo chama **sqlGetInfo** com a opção SQL_ROW_UPDATES.  
  
 [3] **O SQLFetch** só pode retornar esse valor quando ele é misturado com chamadas para **SQLFetchScroll**. Isso porque **o SQLFetch** avança através do conjunto de resultados e, quando é usado exclusivamente, não rebusca nenhuma linha. Como nenhuma linha é rebuscada, **o SQLFetch** não detecta alterações que foram feitas em linhas anteriormente buscadas. No entanto, se **o SQLFetchScroll** posicionar o cursor antes de qualquer linha anteriormente buscada e **o SQLFetch** for usado para buscar essas linhas, **o SQLFetch** poderá detectar quaisquer alterações nessas linhas.  
  
 [4] Devolvido apenas pela SQLBulkOperations. Não definido por **SQLFetch** ou **SQLFetchScroll**.  
  
### <a name="rows-fetched-buffer"></a>Buffer de linhas buscadas  
 O buffer de linhas buscadas é usado para retornar o número de linhas buscadas, incluindo as linhas para as quais nenhum dado foi devolvido porque ocorreu um erro enquanto eles estavam sendo buscados. Em outras palavras, é o número de linhas para as quais o valor na matriz de status da linha não é SQL_ROW_NOROW. O endereço deste buffer é especificado com o atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR. O buffer é alocado pelo aplicativo. Ele é definido por **SQLFetch** e **SQLFetchScroll**. Se o valor do atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR for um ponteiro nulo, essas funções não retornarão o número de linhas buscadas. Para determinar o número da linha atual no conjunto de resultados, um aplicativo pode chamar **SQLGetStmtAttr** com o atributo SQL_ATTR_ROW_NUMBER.  
  
 O conteúdo das linhas de buffer buscadas é indefinido se **SQLFetch** ou **SQLFetchScroll** não retornarSQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, exceto quando SQL_NO_DATA é devolvido, nesse caso o valor nas linhas de buffer buscado é definido como 0.  
  
### <a name="error-handling"></a>Tratamento de erros  
 Erros e avisos podem ser aplicados a linhas individuais ou a toda a função. Para obter mais informações sobre registros de diagnóstico, consulte [Diagnósticos](../../../odbc/reference/develop-app/diagnostics.md) e [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Erros e Avisos em toda a função  
 Se um erro se aplica a toda a função, como SQLSTATE HYT00 (Timeout expired) ou SQLSTATE 24000 (estado cursor inválido), **o SQLFetch** retorna SQL_ERROR e o SQLSTATE aplicável. O conteúdo dos buffers de conjunto de linhas está indefinido e a posição do cursor está inalterada.  
  
 Se um aviso se aplicar a toda a função, **o SQLFetch** retorna SQL_SUCCESS_WITH_INFO e o SQLSTATE aplicável. Os registros de status para avisos que se aplicam a toda a função são retornados antes dos registros de status que se aplicam a linhas individuais.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Erros e Avisos em Linhas Individuais  
 Se um erro (como SQLSTATE 22012 (Divisão por zero)) ou um aviso (como SQLSTATE 01004 (Dados truncados)) se aplicar a uma única linha, **o SQLFetch**faz o seguinte:  
  
-   Define o elemento correspondente da matriz de status da linha para SQL_ROW_ERROR para erros ou SQL_ROW_SUCCESS_WITH_INFO para avisos.  
  
-   Adiciona zero ou mais registros de status que contenham SQLSTATEs para o erro ou aviso.  
  
-   Define os campos de números de linha e coluna nos registros de status. Se **o SQLFetch** não puder determinar um número de linha ou coluna, ele definirá esse número como SQL_ROW_NUMBER_UNKNOWN ou SQL_COLUMN_NUMBER_UNKNOWN, respectivamente. Se o registro de status não se aplicar a uma determinada coluna, **o SQLFetch definirá** o número da coluna como SQL_NO_COLUMN_NUMBER.  
  
 **O SQLFetch** continua buscando linhas até que tenha buscado todas as linhas no conjunto de linhas. Ele retorna SQL_SUCCESS_WITH_INFO a menos que ocorra um erro em todas as linhas do conjunto de linhas (sem incluir linhas com SQL_ROW_NOROW de status), nesse caso ele retorna SQL_ERROR. Em particular, se o tamanho do conjunto de linhas for 1 e ocorrer um erro nessa linha, **o SQLFetch** retorna SQL_ERROR.  
  
 **SQLFetch** retorna os registros de status na ordem de número da linha. Ou seja, ele retorna todos os registros de status para linhas desconhecidas (se houver); em seguida, ele retorna todos os registros de status para a primeira linha (se houver), e então ele retorna todos os registros de status para a segunda linha (se houver), e assim por diante. Os registros de status de cada linha são ordenados de acordo com as regras normais para encomendar registros de status; para obter mais informações, consulte "Seqüência de registros de status" no [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Descritores e SQLFetch  
 As seções a seguir descrevem como **o SQLFetch** interage com descritores.  
  
#### <a name="argument-mappings"></a>Mapeamentos de argumentos  
 O driver não define nenhum campo descritor com base nos argumentos do **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Outros Campos Descritores  
 Os seguintes campos de descritores são usados pelo **SQLFetch**.  
  
|Campo do descritor|Desc.|Campo em|Definido através|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|Ard|cabeçalho|SQL_ATTR_ROW_ARRAY_SIZE atributo de declaração|  
|SQL_DESC_ARRAY_STATUS_PTR|Ird|cabeçalho|SQL_ATTR_ROW_STATUS_PTR atributo de declaração|  
|SQL_DESC_BIND_OFFSET_PTR|Ard|cabeçalho|SQL_ATTR_ROW_BIND_OFFSET_PTR atributo de declaração|  
|SQL_DESC_BIND_TYPE|Ard|cabeçalho|SQL_ATTR_ROW_BIND_TYPE atributo de declaração|  
|SQL_DESC_COUNT|Ard|cabeçalho|*Argumento de número* de coluna **sqlbindcol**|  
|SQL_DESC_DATA_PTR|Ard|records|*Argumento TargetValuePtr* do **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|Ard|records|*StrLen_or_IndPtr* argumento em **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|Ard|records|*Argumento bufferLength* em **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|Ard|records|*StrLen_or_IndPtr* argumento em **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|Ird|cabeçalho|SQL_ATTR_ROWS_FETCHED_PTR atributo de declaração|  
|SQL_DESC_TYPE|Ard|records|*Argumento TargetType* em **SQLBindCol**|  
  
 Todos os campos de descritor também podem ser definidos através **do SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Buffers de comprimento e indicador separados  
 Os aplicativos podem vincular um único buffer ou dois buffers separados que podem ser usados para segurar valores de comprimento e indicador. Quando um aplicativo chama **SQLBindCol**, o driver define os campos SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR do ARD para o mesmo endereço, que é passado no *argumento StrLen_or_IndPtr.* Quando um aplicativo chama **SQLSetDescField** ou **SQLSetDescRec,** ele pode definir esses dois campos para endereços diferentes.  
  
 **O SQLFetch** determina se o aplicativo especificou os buffers de comprimento e indicador separados. Neste caso, quando os dados não são NULAS, **o SQLFetch** define o buffer indicador como 0 e retorna o comprimento no buffer de comprimento. Quando os dados são NUCToS, **o SQLFetch** define o buffer indicador para SQL_NULL_DATA e não modifica o buffer de comprimento.  
  
### <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindCol,](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQLColumns,](../../../odbc/reference/syntax/sqlcolumns-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)e [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Fechando o cursor sobre a declaração|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Buscar parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Retornando o número de colunas de conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparando uma declaração para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
