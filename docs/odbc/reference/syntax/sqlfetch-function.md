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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c5d2d14786080f665e488acf2bfa888f09a5df4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345202"
---
# <a name="sqlfetch-function"></a>Função SQLFetch
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLFetch** busca o próximo conjunto de linhas de dados do conjunto de resultados e retorna dados para todas as colunas associadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLFetch** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando a [função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFetch** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário. Se ocorrer um erro em uma única coluna, [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) poderá ser chamado com um *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que o erro ocorreu; e **SQLGetDiagField** podem ser chamados com um *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
 Para todos os hiperestados que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx sqlstates), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em uma ou mais, mas não em todas as linhas de uma operação multirow, e SQL_ERROR será retornado se ocorrer um erro em um operação de linha única.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Dados de cadeia de caracteres ou binários retornados para uma coluna resultaram no truncamento de um caractere não em branco ou dados binários não nulos. Se fosse um valor de cadeia de caracteres, ele foi truncado à direita.|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas.<br /><br /> (Se esse SQLSTATE for retornado quando um aplicativo ODBC 3 *. x* estiver funcionando com um driver ODBC 2 *. x* , ele poderá ser ignorado.)|  
|01S07|Truncamento fracionário|Os dados retornados para uma coluna foram truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para os tipos de dados time, timestamp e Interval que contêm um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|Não foi possível converter o valor de dados de uma coluna no conjunto de resultados no tipo de dados especificado por *TargetType* em **SQLBindCol**.<br /><br /> A coluna 0 foi associada a um tipo de dados de SQL_C_BOOKMARK, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE.<br /><br /> A coluna 0 foi associada a um tipo de dados de SQL_C_VARBOOKMARK, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS não foi definido como SQL_UB_VARIABLE.|  
|07009|Índice de descritor inválido|O driver era um driver ODBC 2 *. x* que não oferece suporte a **SQLExtendedFetch**e um número de coluna especificado na associação para uma coluna era 0.<br /><br /> A coluna 0 foi associada e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22001|Dados de cadeia de caracteres, truncados à direita|Um indicador de comprimento variável retornado para uma coluna foi truncado.|  
|22002|Variável de indicador necessária, mas não fornecida|Dados nulos foram buscados em uma coluna cujo *StrLen_or_IndPtr* definido por **SQLBindCol** (ou SQL_DESC_INDICATOR_PTR definido por **SQLSetDescField** ou **SQLSetDescRec**) era um ponteiro nulo.|  
|22003|Valor numérico fora do intervalo|Retornar o valor numérico como numérico ou cadeia de caracteres para uma ou mais colunas vinculadas teria causado a parte inteira (em oposição à fração) do número a ser truncado.<br /><br /> Para obter mais informações, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice D: tipos de dados.|  
|22007|Formato de data e hora inválido|Uma coluna de caracteres no conjunto de resultados foi associada a uma estrutura de data, hora ou carimbo de hora C e um valor na coluna era, respectivamente, uma data, hora ou carimbo de hora inválido.|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi retornado, o que resultou em divisão por zero.|  
|22015|Estouro no campo de intervalo|A atribuição de um tipo de SQL numérico ou de intervalo exato para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao buscar dados para um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.|  
|22018|Valor de caractere inválido para especificação de conversão|Uma coluna de caracteres no conjunto de resultados foi associada a um buffer de caractere C e a coluna continha um caractere para o qual não havia nenhuma representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo associado de C.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|40001|Falha de serialização|A transação na qual a busca foi executada foi encerrada para evitar o deadlock.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função **SQLFetch** foi chamada e antes de concluída a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função **SQLFetch** foi chamada novamente no *StatementHandle*.<br /><br /> Ou, a função **SQLFetch** foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLFetch** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) o *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) **SQLFetch** foi chamado para *StatementHandle* depois que **SQLExtendedFetch** foi chamado e antes de **SQLFreeStmt** com a opção SQL_CLOSE foi chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|O atributo da instrução SQL_ATTR_USE_BOOKMARK foi definido como SQL_UB_VARIABLE e a coluna 0 foi associada a um buffer cujo comprimento não era igual ao tamanho máximo do indicador para esse conjunto de resultados. (Esse comprimento está disponível no campo SQL_DESC_OCTET_LENGTH do IRD e pode ser obtido chamando **SQLDescribeCol**, **SQLColAttribute**ou **SQLGetDescField**.)|  
|HY107|Valor da linha fora do intervalo|O valor especificado com o atributo de instrução SQL_ATTR_CURSOR_TYPE foi SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de instrução SQL_ATTR_KEYSET_SIZE era maior que 0 e menor que o valor especificado com o SQL_ATTR_ROW_ARRAY_ Atributo de instrução SIZE.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte à conversão especificada pela combinação de *TargetType* em **SQLBindCol** e o tipo de dados SQL da coluna correspondente.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo limite é definido por meio de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLFetch** retorna o próximo conjunto de linhas no conjunto de resultados. Ele pode ser chamado somente enquanto um conjunto de resultados existir: ou seja, após uma chamada que cria um conjunto de resultados e antes do cursor sobre esse conjunto de resultados ser fechado. Se alguma coluna estiver associada, ela retornará os dados nessas colunas. Se o aplicativo tiver especificado um ponteiro para uma matriz de status de linha ou um buffer no qual retornar o número de linhas buscadas, **SQLFetch** também retornará essas informações. As chamadas para **SQLFetch** podem ser misturadas com chamadas para **SQLFetchScroll** , mas não podem ser misturadas com chamadas para **SQLExtendedFetch**. Para obter mais informações, consulte [buscando uma linha de dados](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Se um aplicativo ODBC*3. x* funcionar com um driver ODBC 2 *. x* , o Gerenciador de driver mapeará chamadas **SQLFetch** para **SQLExtendedFetch** para um driver ODBC 2 *. x* que dá suporte a **SQLExtendedFetch**. Se o driver ODBC 2 *. x* não oferecer suporte a **SQLExtendedFetch**, o Gerenciador de driver mapeará as chamadas **SQLFetch** para **SQLFetch** no driver ODBC 2 *. x* , que pode buscar apenas uma única linha.  
  
 Para obter mais informações, consulte [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
## <a name="positioning-the-cursor"></a>Posicionando o cursor  
 Quando o conjunto de resultados é criado, o cursor é posicionado antes do início do conjunto de resultados. **SQLFetch** busca o próximo conjunto de linhas. É equivalente a chamar **SQLFetchScroll** com *FetchOrientation* definido como SQL_FETCH_NEXT. Para obter mais informações sobre cursores, consulte [cursores](../../../odbc/reference/develop-app/cursors.md) e [cursores de bloco](../../../odbc/reference/develop-app/block-cursors.md).  
  
 O atributo instrução SQL_ATTR_ROW_ARRAY_SIZE especifica o número de linhas no conjunto de linhas. Se o conjunto de linhas que está sendo buscado por **SQLFetch** sobrepor o final do conjunto de resultados, **SQLFetch** retornará um conjunto de linhas parcial. Ou seja, se S + R-1 for maior que L, onde S é a linha inicial do conjunto de linhas que está sendo obtido, R é o tamanho do conjunto de linhas e L é a última linha no conjunto de resultados, somente as primeiras L-S + 1 linhas do conjunto de linhas são válidas. As linhas restantes estão vazias e têm um status de SQL_ROW_NOROW.  
  
 Depois que **SQLFetch** retorna, a linha atual é a primeira linha do conjunto de linhas.  
  
 As regras listadas na tabela a seguir descrevem o posicionamento do cursor após uma chamada para **SQLFetch**, com base nas condições listadas na segunda tabela nesta seção.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|Antes de iniciar|1|  
|** \<CurrRowsetStart =  *LastResultRow-conjunto de*linhas [1]|*CurrRowsetStart* + de*conjunto*de linhas [2]|  
|*CurrRowsetStart* > *LastResultRow-conjunto de*linhas [1]|Após o término|  
|Após o término|Após o término|  
  
 [1] se o tamanho do conjunto de linhas for alterado entre buscas, esse será o tamanho do conjunto de linhas que foi usado com a busca anterior.  
  
 [2] se o tamanho do conjunto de linhas for alterado entre buscas, esse será o tamanho do conjunto de linhas que foi usado com a nova busca.  
  
|Anotações|Significado|  
|--------------|-------------|  
|Antes de iniciar|O cursor de bloco está posicionado antes do início do conjunto de resultados. Se a primeira linha do novo conjunto de linhas for anterior ao início do conjunto de resultados, **SQLFetch** retornará SQL_NO_DATA.|  
|Após o término|O cursor de bloco é posicionado após o final do conjunto de resultados. Se a primeira linha do novo conjunto de linhas for posterior ao final do conjunto de resultados, **SQLFetch** retornará SQL_NO_DATA.|  
|*CurrRowsetStart*|O número da primeira linha no conjunto de linhas atual.|  
|*LastResultRow*|O número da última linha no conjunto de resultados.|  
|*Conjunto de linhas*|O tamanho do conjunto de linhas.|  
  
 Por exemplo, suponha que um conjunto de resultados tenha 100 linhas e o tamanho do conjunto de linhas seja 5. A tabela a seguir mostra o conjunto de linhas e o código de retorno retornados por **SQLFetch** para posições de início diferentes.  
  
|Conjunto de linhas atual|Código de retorno|Novo conjunto de linhas|número de linhas buscadas|  
|--------------------|-----------------|----------------|------------------------|  
|Antes de iniciar|SQL_SUCCESS|1 a 5|5|  
|1 a 5|SQL_SUCCESS|6 a 10|5|  
|52 a 56|SQL_SUCCESS|57 a 61|5|  
|91 a 95|SQL_SUCCESS|96 a 100|5|  
|93 a 97|SQL_SUCCESS|98 a 100. As linhas 4 e 5 da matriz de status de linha são definidas como SQL_ROW_NOROW.|3|  
|96 a 100|SQL_NO_DATA|Nenhum.|0|  
|99 a 100|SQL_NO_DATA|Nenhum.|0|  
|Após o término|SQL_NO_DATA|Nenhum.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Retornando dados em colunas associadas  
 Como **SQLFetch** retorna cada linha, ele coloca os dados de cada coluna associada no buffer associado a essa coluna. Se nenhuma coluna estiver associada, **SQLFetch** não retornará nenhum dado, mas moverá o cursor de bloco para frente. Os dados ainda podem ser recuperados usando **SQLGetData**. Se o cursor for um cursor de LinhaMúltipla (ou seja, o SQL_ATTR_ROW_ARRAY_SIZE for maior que 1), **SQLGetData** poderá ser chamado somente se SQL_GD_BLOCK for retornado quando **SQLGetInfo** for chamado com um *InfoType* de SQL_GETDATA_EXTENSIONS. (Para obter mais informações, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Para cada coluna associada em uma linha, **SQLFetch** faz o seguinte:  
  
1.  Define o buffer de comprimento/indicador como SQL_NULL_DATA e prossegue para a próxima coluna se os dados forem nulos. Se os dados forem nulos e nenhum buffer de comprimento/indicador tiver sido associado, **SQLFetch** retornará SQLSTATE 22002 (variável de indicador necessária, mas não fornecida) para a linha e prosseguir para a próxima linha. Para obter informações sobre como determinar o endereço do buffer de comprimento/indicador, consulte "endereços de buffer" em [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Se os dados da coluna não forem NULL, **SQLFetch** prosseguirá para a etapa 2.  
  
2.  Se o atributo da instrução SQL_ATTR_MAX_LENGTH for definido como um valor diferente de zero e a coluna contiver dados de caractere ou binários, os dados serão truncados para SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  O atributo da instrução SQL_ATTR_MAX_LENGTH destina-se a reduzir o tráfego de rede. Geralmente, ele é implementado pela fonte de dados, o que trunca os dados antes de retorná-los pela rede. Os drivers e as fontes de dados não são necessários para dar suporte a ele. Portanto, para garantir que os dados sejam truncados para um tamanho específico, um aplicativo deve alocar um buffer desse tamanho e especificar o tamanho no argumento *cbValueMax* em **SQLBindCol**.  
  
3.  Converte os dados no tipo especificado por *TargetType* em **SQLBindCol**.  
  
4.  Se os dados foram convertidos em um tipo de dados de comprimento variável, como caractere ou binário, **SQLFetch** verifica se o comprimento dos dados excede o comprimento do buffer de dados. Se o comprimento dos dados de caractere (incluindo o caractere de terminação nula) exceder o comprimento do buffer de dados, **SQLFetch** truncará os dados para o comprimento do buffer de dados menos o comprimento de um caractere de terminação nula. Em seguida, NULL – encerra os dados. Se o comprimento dos dados binários exceder o comprimento do buffer de dados, **SQLFetch** o truncará para o comprimento do buffer de dados. O comprimento do buffer de dados é especificado com *BufferLength* em **SQLBindCol**.  
  
     **SQLFetch** nunca trunca os dados convertidos em tipos de dados de comprimento fixo; Ele sempre pressupõe que o comprimento do buffer de dados é o tamanho do tipo de dados.  
  
5.  Coloca os dados convertidos (e possivelmente truncados) no buffer de dados. Para obter informações sobre como determinar o endereço do buffer de dados, consulte "endereços de buffer" em [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  Coloca o comprimento dos dados no buffer de comprimento/indicador. Se o ponteiro do indicador e o comprimento do ponteiro foram definidos para o mesmo buffer (como uma chamada para **SQLBindCol** ), o comprimento é gravado no buffer para dados válidos e SQL_NULL_DATA é gravado no buffer para dados nulos. Se nenhum buffer de comprimento/indicador tiver sido associado, **SQLFetch** não retornará o comprimento.  
  
    -   Para dados de caracteres ou binários, esse é o comprimento dos dados após a conversão e antes do truncamento porque o buffer de dados é muito pequeno. Se o driver não puder determinar o comprimento dos dados após a conversão, como às vezes é o caso com dados longos, ele definirá o comprimento como SQL_NO_TOTAL. Se os dados foram truncados devido ao atributo da instrução SQL_ATTR_MAX_LENGTH, o valor desse atributo será colocado no buffer de comprimento/indicador, em vez do comprimento real. Isso ocorre porque esse atributo é projetado para truncar dados no servidor antes da conversão, para que o driver não tenha como descobrir qual é o comprimento real.  
  
    -   Para todos os outros tipos de dados, esse é o comprimento dos dados após a conversão; ou seja, é o tamanho do tipo para o qual os dados foram convertidos.  
  
     Para obter informações sobre como determinar o endereço do buffer de comprimento/indicador, consulte "endereços de buffer" em [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Se os dados forem truncados durante a conversão sem perda de dígitos significativos (por exemplo, o número real 1,234 será truncado para o inteiro 1 quando convertido), **SQLFetch** retornará SQLSTATE 01S07 (truncamento fracionário) e SQL_SUCCESS_WITH_INFO. Se os dados estiverem truncados porque o comprimento do buffer de dados é muito pequeno (por exemplo, a cadeia de caracteres "abcdef" é colocada em um buffer de 4 bytes), **SQLFetch** retorna SQLSTATE 01004 (dados truncados) e SQL_SUCCESS_WITH_INFO. Se os dados forem truncados devido ao atributo da instrução SQL_ATTR_MAX_LENGTH, **SQLFetch** retornará SQL_SUCCESS e não retornará SQLSTATE 01S07 (truncamento fracionário) ou SQLSTATE 01004 (dados truncados). Se os dados forem truncados durante a conversão com uma perda de dígitos significativos (por exemplo, se um valor de SQL_INTEGER maior que 100.000 for convertido em um SQL_C_TINYINT), **SQLFetch** retornará SQLSTATE 22003 (valor numérico fora do intervalo) e SQL_ERROR (se o tamanho do conjunto de linhas for 1) ou SQL_SUCCESS_WITH_INFO (se o tamanho do conjunto de linhas for maior que 1).  
  
 O conteúdo do buffer de dados associado e o buffer de comprimento/indicador serão indefinidos se **SQLFetch** ou **SQLFetchScroll** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 A matriz de status de linha é usada para retornar o status de cada linha no conjunto de linhas. O endereço dessa matriz é especificado com o atributo de instrução SQL_ATTR_ROW_STATUS_PTR. A matriz é alocada pelo aplicativo e deve ter tantos elementos quantos forem especificados pelo atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE. Seus valores são definidos por **SQLFetch**, **SQLFetchScroll**e **SQLBulkOperations** ou **SQLSetPos** (exceto quando eles tiverem sido chamados depois que o cursor tiver sido posicionado por **SQLExtendedFetch**). Se o valor do atributo da instrução SQL_ATTR_ROW_STATUS_PTR for NULL, essas funções não retornarão o status da linha.  
  
 O conteúdo do buffer de matriz de status de linha será indefinido se **SQLFetch** ou **SQLFetchScroll** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
 Os valores a seguir são retornados na matriz de status de linha.  
  
|Valor da matriz de status da linha|DESCRIÇÃO|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A linha foi buscada com êxito e não foi alterada desde a última busca deste conjunto de resultados.|  
|SQL_ROW_SUCCESS_WITH_INFO|A linha foi buscada com êxito e não foi alterada desde a última busca deste conjunto de resultados. No entanto, um aviso foi retornado sobre a linha.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED [1], [2] e [3]|A linha foi buscada com êxito e foi alterada desde a última busca deste conjunto de resultados. Se a linha for buscada novamente deste conjunto de resultados ou for atualizada pelo **SQLSetPos**, o status será alterado para o novo status da linha.|  
|SQL_ROW_DELETED [3]|A linha foi excluída desde que foi obtida pela última vez deste conjunto de resultados.|  
|SQL_ROW_ADDED [4]|A linha foi inserida por **SQLBulkOperations**. Se a linha for buscada novamente deste conjunto de resultados ou for atualizada pelo **SQLSetPos**, seu status será SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|O conjunto de linhas sobreposto ao final do conjunto de resultados e nenhuma linha foi retornada correspondente a esse elemento da matriz de status de linha.|  
  
 [1] para cursores de conjunto de chaves, mistos e dinâmicos, se um valor de chave for atualizado, a linha de dados será considerada como excluída e uma nova linha adicionada.  
  
 [2] alguns drivers não podem detectar atualizações nos dados e, portanto, não podem retornar esse valor. Para determinar se um driver pode detectar atualizações para linhas rebuscadas, um aplicativo chama **SQLGetInfo** com a opção SQL_ROW_UPDATES.  
  
 [3] **SQLFetch** pode retornar esse valor somente quando ele é misturado com chamadas para **SQLFetchScroll**. Isso ocorre porque o **SQLFetch** avança pelo conjunto de resultados e, quando é usado exclusivamente, não rebusca nenhuma linha. Como nenhuma linha é rebuscada, **SQLFetch** não detecta alterações que foram feitas em linhas previamente buscadas. No entanto, se **SQLFetchScroll** posicionar o cursor antes de qualquer linha previamente buscada e **SQLFetch** for usado para buscar essas linhas, **SQLFetch** poderá detectar qualquer alteração nessas linhas.  
  
 [4] retornado somente por SQLBulkOperations. Não definido por **SQLFetch** ou **SQLFetchScroll**.  
  
### <a name="rows-fetched-buffer"></a>Buffers buscados de linhas  
 O buffer de linhas buscadas é usado para retornar o número de linhas buscadas, incluindo as linhas para as quais nenhum dado foi retornado porque ocorreu um erro enquanto ele estava sendo buscado. Em outras palavras, é o número de linhas para as quais o valor na matriz de status de linha não é SQL_ROW_NOROW. O endereço desse buffer é especificado com o atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR. O buffer é alocado pelo aplicativo. Ele é definido por **SQLFetch** e **SQLFetchScroll**. Se o valor do atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR for um ponteiro NULL, essas funções não retornarão o número de linhas buscadas. Para determinar o número da linha atual no conjunto de resultados, um aplicativo pode chamar **SQLGetStmtAttr** com o atributo SQL_ATTR_ROW_NUMBER.  
  
 O conteúdo das linhas de buffer buscadas será indefinido se **SQLFetch** ou **SQLFetchScroll** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, exceto quando SQL_NO_DATA for retornado; nesse caso, o valor no buffer de linhas buscados será definido como 0.  
  
### <a name="error-handling"></a>Tratamento de erros  
 Erros e avisos podem ser aplicados a linhas individuais ou a toda a função. Para obter mais informações sobre registros de diagnóstico, consulte [Diagnostics](../../../odbc/reference/develop-app/diagnostics.md) and [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Erros e avisos sobre a função inteira  
 Se um erro se aplicar a toda a função, como SQLSTATE HYT00 (timeout expirado) ou SQLSTATE 24000 (estado de cursor inválido), **SQLFetch** retornará SQL_ERROR e o SQLSTATE aplicável. O conteúdo dos buffers de conjunto de linhas é indefinido e a posição do cursor não é alterada.  
  
 Se um aviso se aplicar a toda a função, **SQLFetch** retornará SQL_SUCCESS_WITH_INFO e o SQLSTATE aplicável. Os registros de status para avisos que se aplicam a toda a função são retornados antes dos registros de status que se aplicam a linhas individuais.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Erros e avisos em linhas individuais  
 Se um erro (como SQLSTATE 22012 (divisão por zero)) ou um aviso (como SQLSTATE 01004 (dados truncados)) se aplicar a uma única linha, **SQLFetch**fará o seguinte:  
  
-   Define o elemento correspondente da matriz de status de linha para SQL_ROW_ERROR erros ou SQL_ROW_SUCCESS_WITH_INFO para avisos.  
  
-   Adiciona zero ou mais registros de status que contêm sqlstates para o erro ou aviso.  
  
-   Define os campos de número de linha e coluna nos registros de status. Se **SQLFetch** não puder determinar um número de linha ou coluna, ele definirá esse número como SQL_ROW_NUMBER_UNKNOWN ou SQL_COLUMN_NUMBER_UNKNOWN, respectivamente. Se o registro de status não se aplicar a uma determinada coluna, **SQLFetch** definirá o número da coluna como SQL_NO_COLUMN_NUMBER.  
  
 **SQLFetch** continua buscando linhas até que tenha buscado todas as linhas no conjunto de linhas. Ele retorna SQL_SUCCESS_WITH_INFO, a menos que ocorra um erro em cada linha do conjunto de linhas (não incluindo linhas com o status SQL_ROW_NOROW). nesse caso, ela retorna SQL_ERROR. Em particular, se o tamanho do conjunto de linhas for 1 e ocorrer um erro nessa linha, **SQLFetch** retornará SQL_ERROR.  
  
 **SQLFetch** retorna os registros de status na ordem de números de linha. Ou seja, ele retorna todos os registros de status de linhas desconhecidas (se houver); em seguida, ele retorna todos os registros de status para a primeira linha (se houver) e, em seguida, retorna todos os registros de status da segunda linha (se houver) e assim por diante. Os registros de status para cada linha são ordenados de acordo com as regras normais para ordenar registros de status; para obter mais informações, consulte "sequência de registros de status" em [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Descritores e SQLFetch  
 As seções a seguir descrevem como o **SQLFetch** interage com os descritores.  
  
#### <a name="argument-mappings"></a>Mapeamentos de argumento  
 O driver não define nenhum campo de descritor com base nos argumentos de **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Outros campos de descritor  
 Os seguintes campos de descritor são usados por **SQLFetch**.  
  
|Campo do descritor|Crescente.|Campo em|Definir por|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ARD|cabeçalho|Atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|cabeçalho|Atributo de instrução SQL_ATTR_ROW_STATUS_PTR|  
|SQL_DESC_BIND_OFFSET_PTR|ARD|cabeçalho|Atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_DESC_BIND_TYPE|ARD|cabeçalho|Atributo de instrução SQL_ATTR_ROW_BIND_TYPE|  
|SQL_DESC_COUNT|ARD|cabeçalho|Argumento *ColumnNumber* de **SQLBindCol**|  
|SQL_DESC_DATA_PTR|ARD|records|Argumento *TargetValuePtr* de **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|ARD|records|*StrLen_or_IndPtr* argumento em **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|ARD|records|Argumento *BufferLength* em **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|ARD|records|*StrLen_or_IndPtr* argumento em **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|cabeçalho|Atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR|  
|SQL_DESC_TYPE|ARD|records|Argumento *TargetType* em **SQLBindCol**|  
  
 Todos os campos de descritor também podem ser definidos por meio de **SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Buffers de comprimento e indicador separados  
 Os aplicativos podem associar um único buffer ou dois buffers separados que podem ser usados para conter valores de comprimento e indicador. Quando um aplicativo chama **SQLBindCol**, o driver define os campos SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR do ARD para o mesmo endereço, que é passado no argumento *StrLen_or_IndPtr* . Quando um aplicativo chama **SQLSetDescField** ou **SQLSetDescRec**, ele pode definir esses dois campos como endereços diferentes.  
  
 **SQLFetch** determina se o aplicativo especificou buffers de comprimento e de indicador separados. Nesse caso, quando os dados não são nulos, **SQLFetch** define o buffer do indicador como 0 e retorna o comprimento no buffer de comprimento. Quando os dados são nulos, **SQLFetch** define o buffer do indicador como SQL_NULL_DATA e não modifica o buffer de comprimento.  
  
### <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)e [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Fechando o cursor na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Buscando parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Retornando o número de colunas do conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparando uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
