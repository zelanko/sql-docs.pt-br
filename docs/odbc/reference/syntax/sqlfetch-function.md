---
title: Função SQLFetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3af90114b88e3f54f14bbb94357f4f3bf805bb30
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfetch-function"></a>Função SQLFetch
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLFetch** busca o próximo conjunto de linhas de dados do conjunto de resultados e retorna dados para todas as colunas associadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLFetch** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando [função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) com um *HandleType*sql_handle_stmt e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFetch** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário. Se ocorrer um erro em uma única coluna, [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) pode ser chamado com um *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar a coluna em que o erro ocorreu em; e  **SQLGetDiagField** pode ser chamado com um *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
 Para todos esses SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em uma ou mais, mas nem todas as linhas de uma operação de multilinha e SQL_ERROR será retornado se ocorrer um erro em um operação de única linha.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Cadeia de caracteres ou dados binários retornados para uma coluna resultaram em truncamento de caracteres não vazia ou dados binários não nulo. Se fosse um valor de cadeia de caracteres, foi truncado à direita.|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas.<br /><br /> (Se este SQLSTATE é retornado quando um ODBC 3*. x* aplicativo estiver trabalhando com um ODBC 2*. x* driver, ele pode ser ignorado.)|  
|01S07|Truncamento fracionário|Os dados retornados de uma coluna foi truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para o tempo, carimbo de hora e tipos de dados de intervalo que contêm um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor dos dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado por *TargetType* na **SQLBindCol**.<br /><br /> A coluna 0 foi associada com um tipo de dados de SQL_C_BOOKMARK, e o atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE.<br /><br /> A coluna 0 foi associada com um tipo de dados de SQL_C_VARBOOKMARK, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS não foi definido para SQL_UB_VARIABLE.|  
|07009|Índice do descritor inválido|O driver foi um ODBC 2*. x* driver não oferece suporte a **SQLExtendedFetch**, e um número de coluna especificado na associação para uma coluna era 0.<br /><br /> A coluna 0 foi associada e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22001|Dados de cadeia de caracteres truncados à direita|Um indicador de comprimento variável retornado para uma coluna foi truncado.|  
|22002|Variável de indicador exigida mas não fornecida|Dados nulos foi encontrados em uma coluna cujo *StrLen_or_IndPtr* definido por **SQLBindCol** (ou SQL_DESC_INDICATOR_PTR definido por **SQLSetDescField** ou  **SQLSetDescRec**) foi um ponteiro nulo.|  
|22003|Valor numérico fora do intervalo|Retornar o valor numérico como numérico ou cadeia de caracteres para uma ou mais colunas associadas causaria parte inteira (em vez de frações) o número a ser truncado.<br /><br /> Para obter mais informações, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice d: os tipos de dados.|  
|22007|Formato de datetime inválido|Uma coluna de caractere no conjunto de resultados foi associada a uma data, hora ou estrutura de carimbo de hora C, e um valor na coluna foi, respectivamente, uma data inválida, hora ou carimbo de hora.|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi retornado, resultando na divisão por zero.|  
|22015|Estouro no campo de intervalo|Atribuição de um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao buscar dados para um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.|  
|22018|Valor de caractere inválido para especificação de coerção|Uma coluna de caractere no conjunto de resultados foi associada a um buffer de caractere C e a coluna contém um caractere para os quais não houve nenhuma representação no conjunto de caracteres do buffer.<br /><br /> O tipo C foi um numérico exato ou aproximado, uma data e hora ou um tipo de dados do intervalo; o tipo SQL da coluna era de um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo C associado.|  
|24000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado mas nenhum conjunto de resultados foi associado a *StatementHandle*.|  
|40001|Falha na serialização|A transação na qual a busca foi executada foi encerrada para evitar bloqueio.|  
|40003|Conclusão de instrução desconhecido|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. O **SQLFetch** função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, o **SQLFetch** função foi chamada novamente no *StatementHandle*.<br /><br /> Ou, o **SQLFetch** função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*  de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLFetch** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) especificado *StatementHandle* não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) **SQLFetch** foi chamado para o *StatementHandle* depois **SQLExtendedFetch** foi chamado e antes de **SQLFreeStmt** com o SQL _ Opção CLOSE foi chamada.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|O atributo da instrução SQL_ATTR_USE_BOOKMARK foi definido como SQL_UB_VARIABLE, e a coluna 0 foi associada a um buffer cujo comprimento não era igual ao comprimento máximo para o indicador para esse conjunto de resultados. (Esse comprimento está disponível no campo SQL_DESC_OCTET_LENGTH do ird e pode ser obtido chamando **SQLDescribeCol**, **SQLColAttribute**, ou **SQLGetDescField**.)|  
|HY107|Valor de linha fora do intervalo|O valor especificado com o atributo de instrução SQL_ATTR_CURSOR_TYPE era SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo de instrução SQL_ATTR_KEYSET_SIZE era maior que 0 e menor que o valor especificado com o SQL_ATTR_ROW_ARRAY_ Atributo de instrução de tamanho.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não suporta a conversão especificada pela combinação da *TargetType* na **SQLBindCol** e o tipo de dados SQL da coluna correspondente.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornada este conjunto de resultado solicitada. O período de tempo limite é definido por meio de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLFetch** retorna o próximo conjunto de linhas no conjunto de resultados. Ele pode ser chamado apenas enquanto existe um conjunto de resultados: ou seja, depois de uma chamada que cria um conjunto de resultados e antes do cursor é fechado por que o conjunto de resultados. Se todas as colunas associadas, ele retorna os dados nessas colunas. Se o aplicativo tiver especificado um ponteiro para uma matriz de status de linha ou um buffer no qual retornar o número de linhas buscadas, **SQLFetch** também retorna essas informações. Chamadas para **SQLFetch** podem ser misturadas a chamadas para **SQLFetchScroll** , mas não podem ser misturadas a chamadas para **SQLExtendedFetch**. Para obter mais informações, consulte [buscar uma linha de dados](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Se um ODBC 3*. x* aplicativo funciona com um ODBC 2*. x* driver, o Gerenciador de Driver mapeia **SQLFetch** chamadas para **SQLExtendedFetch** para um ODBC 2*. x* driver dá suporte a **SQLExtendedFetch**. Se o ODBC 2*. x* driver não dá suporte **SQLExtendedFetch**, o Gerenciador de Driver mapeia **SQLFetch** chamadas para **SQLFetch** no ODBC 2 *. x* driver, que pode buscar somente uma única linha.  
  
 Para obter mais informações, consulte [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
## <a name="positioning-the-cursor"></a>Posicionando o Cursor  
 Quando o conjunto de resultados é criado, o cursor é posicionado antes do início do conjunto de resultados. **SQLFetch** busca o próximo conjunto de linhas. É equivalente a chamar **SQLFetchScroll** com *FetchOrientation* definido como SQL_FETCH_NEXT. Para obter mais informações sobre cursores, consulte [cursores](../../../odbc/reference/develop-app/cursors.md) e [cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md).  
  
 O atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE Especifica o número de linhas no conjunto de linhas. Se o conjunto de linhas que estão sendo buscadas por **SQLFetch** sobrepõe o fim do conjunto de resultados, **SQLFetch** retorna um conjunto de linhas parcial. Ou seja, se S + R-1 é maior que L, onde S é a linha inicial do conjunto de linhas sendo buscado, R é o tamanho do conjunto de linhas e L é a última linha no conjunto de resultados, em seguida, somente o primeiro L – S + 1 linhas do conjunto de linhas são válidos. As linhas restantes estão vazias e tem um status de SQL_ROW_NOROW.  
  
 Depois de **SQLFetch** retorna, a linha atual é a primeira linha do conjunto de linhas.  
  
 As regras listadas na tabela a seguir descrevem o posicionamento do cursor após uma chamada para **SQLFetch**, com base nas condições listadas na segunda tabela nesta seção.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|Antes de iniciar|1|  
|*CurrRowsetStart* \< =  *LastResultRow – RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow – RowsetSize*[1]|Após o término|  
|Após o término|Após o término|  
  
 [1] se o tamanho do conjunto de linhas for alterado entre buscas, esse é o tamanho do conjunto de linhas que foi usado com a busca anterior.  
  
 [2] se o tamanho do conjunto de linhas for alterado entre buscas, esse é o tamanho do conjunto de linhas que foi usado com a nova busca.  
  
|Notação|Significado|  
|--------------|-------------|  
|Antes de iniciar|O cursor em bloco é posicionado antes do início do conjunto de resultados. Se for a primeira linha do novo conjunto de linhas antes do início do conjunto de resultados, **SQLFetch** retorna SQL_NO_DATA.|  
|Após o término|O cursor em bloco é posicionado após o final do resultado definido. Se for a primeira linha do novo conjunto de linhas após o final do conjunto de resultados, **SQLFetch** retorna SQL_NO_DATA.|  
|*CurrRowsetStart*|O número da primeira linha no conjunto de linhas atual.|  
|*LastResultRow*|O número da última linha no conjunto de resultados.|  
|*RowsetSize*|O tamanho do conjunto de linhas.|  
  
 Por exemplo, suponha que um conjunto de resultados tem 100 linhas e o tamanho do conjunto de linhas é 5. A tabela a seguir mostra o código de conjunto de linhas e de retorno retornado por **SQLFetch** para diferentes posições iniciais.  
  
|Conjunto de linhas atual|Código de retorno|Novo conjunto de linhas|número de linhas buscadas|  
|--------------------|-----------------|----------------|------------------------|  
|Antes de iniciar|SQL_SUCCESS|1 a 5|5|  
|1 a 5|SQL_SUCCESS|6 a 10|5|  
|52 para 56|SQL_SUCCESS|57 para 61|5|  
|91 a 95|SQL_SUCCESS|96 a 100|5|  
|93 para 97|SQL_SUCCESS|98 a 100. Linhas 4 e 5 da matriz de status de linha são definidas como SQL_ROW_NOROW.|3|  
|96 a 100|SQL_NO_DATA|Nenhum.|0|  
|99 a 100|SQL_NO_DATA|Nenhum.|0|  
|Após o término|SQL_NO_DATA|Nenhum.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Retornando dados em colunas associadas  
 Como **SQLFetch** retorna cada linha, ele coloca os dados para cada coluna associada no buffer associado a essa coluna. Se não há colunas associadas, **SQLFetch** Avançar o cursor em bloco, mas não retorna nenhum dado. Os dados ainda podem ser recuperados usando **SQLGetData**. Se o cursor é multilinha (ou seja, se SQL_ATTR_ROW_ARRAY_SIZE for maior que 1), **SQLGetData** pode ser chamado somente se SQL_GD_BLOCK é retornado quando **SQLGetInfo** é chamado com um  *Tipo de informação* de SQL_GETDATA_EXTENSIONS. (Para obter mais informações, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Para cada coluna associada em uma linha, **SQLFetch** faz o seguinte:  
  
1.  Define o buffer de comprimento/indicador como SQL_NULL_DATA e vai para a próxima coluna se os dados são NULL. Se os dados são NULL e nenhum buffer de comprimento/indicador foi associado, **SQLFetch** retornará SQLSTATE 22002 (variável de indicador necessária, mas não fornecida) para a linha e vai para a próxima linha. Para obter informações sobre como determinar o endereço do buffer de comprimento/indicador, consulte "Endereços de Buffer" [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Se os dados para a coluna não forem NULL, **SQLFetch** continua com a etapa 2.  
  
2.  Se o atributo da instrução SQL_ATTR_MAX_LENGTH é definido como um valor diferente de zero e a coluna contém caracteres ou dados binários, os dados são truncados para bytes SQL_ATTR_MAX_LENGTH.  
  
    > [!NOTE]  
    >  O atributo da instrução SQL_ATTR_MAX_LENGTH destina-se a reduzir o tráfego de rede. Ele geralmente é implementado pela fonte de dados, que trunca os dados antes de retorná-lo pela rede. Drivers e fontes de dados não são necessários para dar suporte a ele. Portanto, para garantir que os dados são truncados para um tamanho específico, um aplicativo deve alocar um buffer de tamanho e especifique o tamanho no *cbValueMax* argumento **SQLBindCol**.  
  
3.  Converte os dados para o tipo especificado pelo *TargetType* na **SQLBindCol**.  
  
4.  Se os dados foi convertidos em um tipo de dados de comprimento variável, como caractere ou binário, **SQLFetch** verifica se o comprimento dos dados excede o comprimento do buffer de dados. Se o comprimento dos dados de caracteres (incluindo o caractere null de terminação) excede o comprimento do buffer de dados, **SQLFetch** truncará os dados para o comprimento do buffer de dados, menos o comprimento de um caractere null de terminação. Em seguida, null-encerra os dados. Se o comprimento dos dados binários excede o comprimento do buffer de dados, **SQLFetch** trunca o comprimento do buffer de dados. O comprimento do buffer de dados é especificado com *BufferLength* na **SQLBindCol**.  
  
     **SQLFetch** nunca trunca os dados convertidos para dados de comprimento fixo tipos; ele sempre pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados.  
  
5.  Coloca os dados convertidos (e possivelmente truncados) no buffer de dados. Para obter informações sobre como determinar o endereço do buffer de dados, consulte "Endereços de Buffer" [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  Coloca o comprimento dos dados no buffer de comprimento/indicador. Se o ponteiro do indicador e o ponteiro de comprimento foram definidas para o mesmo buffer (como uma chamada para **SQLBindCol** does), o comprimento é gravado no buffer de dados válidos e SQL_NULL_DATA é gravado no buffer de dados NULL. Se nenhum buffer de comprimento/indicador foi associado, **SQLFetch** não retorna o comprimento.  
  
    -   Para caracteres ou dados binários, esse é o comprimento dos dados após a conversão e antes de truncamento devido a buffer de dados é muito pequeno. Se o driver não pode determinar o comprimento dos dados após a conversão, como às vezes é o caso com dados longos, ele define o comprimento para SQL_NO_TOTAL. Se os dados foram truncados devido o atributo da instrução SQL_ATTR_MAX_LENGTH, o valor desse atributo é colocado no buffer de comprimento/indicador, em vez do comprimento real. Isso ocorre porque esse atributo foi projetado para truncar os dados no servidor antes da conversão, para que o driver não tem como descobrir o que é o comprimento real.  
  
    -   Para todos os outros tipos de dados, esse é o comprimento dos dados após a conversão; ou seja, ele é o tamanho do tipo para o qual os dados foi convertidos.  
  
     Para obter informações sobre como determinar o endereço do buffer de comprimento/indicador, consulte "Endereços de Buffer" [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Se os dados são truncados durante conversão sem uma perda de dígitos significativos (por exemplo, o número real 1,234 é truncado para o inteiro 1 quando convertido), **SQLFetch** retornará SQLSTATE 01S07 (Truncamento fracionário) e SQL _ SUCCESS_WITH_INFO. Se os dados são truncados porque o comprimento do buffer de dados é muito pequeno (por exemplo, a cadeia de caracteres "abcdef" é colocada em um buffer de 4 bytes), **SQLFetch** retorna SQL_SUCCESS_WITH_INFO e o SQLSTATE 01004 (dados truncados). Se os dados são truncados devido o atributo da instrução SQL_ATTR_MAX_LENGTH, **SQLFetch** retorna SQL_SUCCESS e não retornará SQLSTATE 01S07 (Truncamento fracionário) ou SQLSTATE 01004 (dados truncados). Se os dados são truncados durante conversão com perda de dígitos significativos (por exemplo, se um valor SQL_INTEGER maior que 100.000 foram convertido em um SQL_C_TINYINT), **SQLFetch** retornará SQLSTATE 22003 (valor numérico fora do intervalo) e (se o tamanho do conjunto de linhas é 1) de SQL_ERROR ou SQL_SUCCESS_WITH_INFO (se o tamanho do conjunto de linhas é maior que 1).  
  
 O conteúdo do buffer de dados associados e o buffer de comprimento/indicador é indefinido se **SQLFetch** ou **SQLFetchScroll** não retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
## <a name="row-status-array"></a>Matriz de Status de linha  
 A matriz de status de linha é usada para retornar o status de cada linha no conjunto de linhas. O endereço desta matriz é especificado com o atributo de instrução SQL_ATTR_ROW_STATUS_PTR. A matriz alocada pelo aplicativo e deve ter elementos são especificadas pelo atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE. Seus valores são definidos pelo **SQLFetch**, **SQLFetchScroll**, e **SQLBulkOperations** ou **SQLSetPos** (exceto quando foi chamados Depois que o cursor tiver sido posicionado por **SQLExtendedFetch**). Se o valor do atributo de instrução sql_attr_row_status_ptr de modo que é um ponteiro nulo, essas funções não retornam o status de linha.  
  
 O conteúdo do buffer de matriz de status de linha serão definido se **SQLFetch** ou **SQLFetchScroll** não retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
 Os seguintes valores são retornados na matriz de status de linha.  
  
|Valor de matriz de status de linha|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A linha foi obtida com êxito e não alterados desde a última busca do conjunto de resultados.|  
|SQL_ROW_SUCCESS_WITH_INFO|A linha foi obtida com êxito e não alterados desde a última busca do conjunto de resultados. No entanto, um aviso sobre a linha foi retornado.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED [1], [2] e [3]|A linha foi obtida com êxito e foi alterado desde a última busca do conjunto de resultados. Se a linha é novamente buscada deste conjunto de resultados ou é atualizada por **SQLSetPos**, o status é alterado para o status da linha nova.|  
|SQL_ROW_DELETED [3]|A linha foi excluída desde a última busca do conjunto de resultados.|  
|SQL_ROW_ADDED [4]|A linha foi inserida por **SQLBulkOperations**. Se a linha é novamente buscada deste conjunto de resultados ou é atualizada por **SQLSetPos**, seu status é SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|O conjunto de linhas sobrepostos final do conjunto de resultados, e nenhuma linha foi retornada que correspondeu a esse elemento da matriz de status de linha.|  
  
 [1] para o conjunto de chaves, mistos e dinâmicos cursores, se um valor de chave for atualizado, a linha de dados é considerada para ter sido excluída e uma nova linha adicionada.  
  
 [2] alguns drivers não poderão detectar atualizações aos dados e, portanto, não é possível retornar esse valor. Para determinar se um driver pode detectar as atualizações para linhas refetched, um aplicativo chama **SQLGetInfo** com a opção SQL_ROW_UPDATES.  
  
 [3] **SQLFetch** pode retornar esse valor somente quando for mesclado com chamadas para **SQLFetchScroll**. Isso ocorre porque **SQLFetch** avança o conjunto de resultados e quando ela é usada exclusivamente, não buscar novamente todas as linhas. Porque nenhuma linha é refetched, **SQLFetch** não detecta alterações que foram feitas nas linhas buscadas anteriormente. No entanto, se **SQLFetchScroll** posiciona o cursor antes de qualquer buscado previamente linhas e **SQLFetch** é usado para buscar as linhas **SQLFetch** pode detectar todas as alterações Essas linhas.  
  
 [4] retornado por SQLBulkOperations somente. Não definido por **SQLFetch** ou **SQLFetchScroll**.  
  
### <a name="rows-fetched-buffer"></a>Buffer de busca de linhas  
 As linhas buscadas buffer é usado para retornar o número de linhas buscadas, incluindo as linhas para que nenhum dado foi retornado porque ocorreu um erro enquanto eles estão sendo buscados. Em outras palavras, é o número de linhas para o qual o valor da matriz de status de linha não é SQL_ROW_NOROW. O endereço desse buffer é especificado com o atributo SQL_ATTR_ROWS_FETCHED_PTR de instrução. O buffer é alocado pelo aplicativo. Ele é definido por **SQLFetch** e **SQLFetchScroll**. Se o valor do atributo SQL_ATTR_ROWS_FETCHED_PTR instrução é um ponteiro nulo, essas funções não retornam o número de linhas buscadas. Para determinar o número da linha atual no conjunto de resultados, um aplicativo pode chamar **SQLGetStmtAttr** com o atributo SQL_ATTR_ROW_NUMBER.  
  
 O conteúdo do buffer de linhas buscadas é indefinido se **SQLFetch** ou **SQLFetchScroll** não retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, exceto quando SQL_NO_DATA for retornado, caso em que o o valor nas linhas buscadas buffer é definido como 0.  
  
### <a name="error-handling"></a>Tratamento de erros  
 Erros e avisos podem aplicar em linhas individuais ou para a função inteira. Para obter mais informações sobre os registros de diagnóstico, consulte [diagnóstico](../../../odbc/reference/develop-app/diagnostics.md) e [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Erros e avisos sobre a função inteira  
 Se um erro se aplica à função inteira, como o SQLSTATE HYT00 (tempo limite expirado) ou SQLSTATE 24000 (estado de cursor inválido), **SQLFetch** retornará SQL_ERROR e o SQLSTATE aplicável. O conteúdo dos buffers de linhas é indefinido e a posição do cursor é alterada.  
  
 Se um aviso se aplica a função inteira, **SQLFetch** retorna SQL_SUCCESS_WITH_INFO e o SQLSTATE aplicável. Os registros de status de avisos que se aplicam a função inteira são retornados antes dos registros de status que se aplicam a linhas individuais.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Erros e avisos em linhas individuais  
 Se um erro (por exemplo, um SQLSTATE 22012 (divisão por zero)) ou um aviso (como o SQLSTATE 01004 (dados truncados)) que se aplica a uma única linha, **SQLFetch**faz o seguinte:  
  
-   Define o elemento correspondente da matriz de status de linha para SQL_ROW_ERROR erros ou SQL_ROW_SUCCESS_WITH_INFO avisos.  
  
-   Adiciona a zero ou mais registros de status que contêm SQLSTATEs para o erro ou aviso.  
  
-   Define os campos de número de linhas e colunas dos registros de status. Se **SQLFetch** não é possível determinar um número de linha ou coluna, ele define esse número para SQL_ROW_NUMBER_UNKNOWN ou SQL_COLUMN_NUMBER_UNKNOWN, respectivamente. Se o registro de status não se aplica a uma coluna específica, **SQLFetch** define o número de coluna como SQL_NO_COLUMN_NUMBER.  
  
 **SQLFetch** continua a busca de linhas até que ele busca todas as linhas no conjunto de linhas. Ele retornará SQL_SUCCESS_WITH_INFO, a menos que ocorra um erro em cada linha do conjunto de linhas (não incluindo linhas com status SQL_ROW_NOROW), caso em que ele retornará SQL_ERROR. Em particular, se o tamanho do conjunto de linhas é 1 e ocorre um erro na linha, **SQLFetch** retornará SQL_ERROR.  
  
 **SQLFetch** retorna os registros de status em ordem de número de linha. Ou seja, ela retorna todos os registros de status para linhas desconhecidos (se houver); em seguida ele retorna todos os registros de status para a primeira linha (se houver) e, em seguida, ele retorna todos os registros de status para a segunda linha (se houver) e assim por diante. Os registros de status para cada linha são ordenados de acordo com as regras normais de ordenação de registros de status. Para obter mais informações, consulte "Sequência de registros de Status" em [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Descritores e SQLFetch  
 As seções a seguir descrevem como **SQLFetch** interage com descritores.  
  
#### <a name="argument-mappings"></a>Mapeamentos de argumento  
 O driver não define os campos de descritor com base em argumentos de **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Outros campos de descritor  
 Os seguintes campos de descritor são usados por **SQLFetch**.  
  
|Campo do descritor|Desc.|Campo|Definido por meio de|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|DESCARTAR|Cabeçalho|Atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|Cabeçalho|Atributo de instrução SQL_ATTR_ROW_STATUS_PTR|  
|SQL_DESC_BIND_OFFSET_PTR|DESCARTAR|Cabeçalho|Atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_DESC_BIND_TYPE|DESCARTAR|Cabeçalho|Atributo de instrução SQL_ATTR_ROW_BIND_TYPE|  
|SQL_DESC_COUNT|DESCARTAR|Cabeçalho|*ColumnNumber* argumento de **SQLBindCol**|  
|SQL_DESC_DATA_PTR|DESCARTAR|Registros|*TargetValuePtr* argumento de **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|DESCARTAR|Registros|*StrLen_or_IndPtr* argumento **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|DESCARTAR|Registros|*BufferLength* argumento **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|DESCARTAR|Registros|*StrLen_or_IndPtr* argumento **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|Cabeçalho|Atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR|  
|SQL_DESC_TYPE|DESCARTAR|Registros|*TargetType* argumento **SQLBindCol**|  
  
 Todos os campos de descritor também podem ser definidos por meio de **SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Comprimento separado e Buffers de indicador  
 Aplicativos podem associar um único buffer ou dois buffers separados que podem ser usados para armazenar valores de comprimento e indicador. Quando um aplicativo chama **SQLBindCol**, o driver define os campos SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR da descartar para o mesmo endereço, que é passado a *StrLen_or_IndPtr* argumento. Quando um aplicativo chama **SQLSetDescField** ou **SQLSetDescRec**, ele pode definir esses dois campos para endereços diferentes.  
  
 **SQLFetch** determina se o aplicativo especificou buffers de tamanho e indicador separados. Nesse caso, quando os dados não forem nulos, **SQLFetch** define o buffer indicador para 0 e retorna o comprimento do buffer de comprimento. Quando os dados são NULL, **SQLFetch** define o buffer de indicador como SQL_NULL_DATA e não a modifica o buffer de comprimento.  
  
### <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), e [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Fechar cursor na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Busca de parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Colunas do conjunto de retorno do número de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
