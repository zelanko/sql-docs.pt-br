---
title: Função SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0dc0e57356c972797cbd72fa4ce3427a0e473dad
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537996"
---
# <a name="sqlgetdata-function"></a>Função SQLGetData
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLGetData** recupera dados para uma única coluna no conjunto de resultados ou para um único parâmetro após **SQLParamData** retorna SQL_PARAM_DATA_AVAILABLE. Ele pode ser chamado várias vezes para recuperar dados de comprimento variável em partes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *Col_or_Param_Num*  
 [Entrada] Para recuperar dados da coluna, ele é o número da coluna para a qual retornar dados. Colunas do conjunto de resultados são numeradas em ordem crescente de coluna começando em 1. A coluna de indicador é o número da coluna 0; Isso pode ser especificado somente se os indicadores estão habilitados.  
  
 Para recuperar dados de parâmetro, é o ordinal do parâmetro, que começa em 1.  
  
 *TargetType*  
 [Entrada] O identificador de tipo do tipo de dados C a **TargetValuePtr* buffer. Para obter uma lista de tipos de dados válidos do C e identificadores de tipo, consulte o [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) seção no Apêndice d: Tipos de dados.  
  
 Se *TargetType* é SQL_ARD_TYPE, o driver utiliza o identificador do tipo especificado no campo SQL_DESC_CONCISE_TYPE da descartar. Se *TargetType* é SQL_APD_TYPE, **SQLGetData** usará o mesmo tipo de dados de C que foi especificado na **SQLBindParameter**. Caso contrário, o tipo de dados C é especificado na **SQLGetData** substitui o tipo de dados C especificado em **SQLBindParameter**. Se for SQL_C_DEFAULT, o driver seleciona o tipo de dados C padrão com base no tipo da fonte de dados SQL.  
  
 Você também pode especificar um tipo de dados estendido C. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Saída] Ponteiro para o buffer no qual retornar os dados.  
  
 *TargetValuePtr* não pode ser NULL.  
  
 *BufferLength*  
 [Entrada] Comprimento do **TargetValuePtr* buffer em bytes.  
  
 O driver usa *BufferLength* para evitar a escrita após o término da \* *TargetValuePtr* buffer ao retornar dados de comprimento variável, como caractere ou dados binários. Observe que o driver conta o caractere de finalização null ao retornar dados de caractere \* *TargetValuePtr*. **TargetValuePtr* , portanto, deve conter espaço para o caractere nulo de terminação, ou o driver irá truncar os dados.  
  
 Quando o driver retorna dados de comprimento fixo, como um inteiro ou uma estrutura de data, o driver ignorará *BufferLength* e pressupõe que o buffer é grande o suficiente para manter os dados. Portanto, é importante para o aplicativo alocar um buffer grande o suficiente para dados de comprimento fixo ou o driver irá escrever após o fim do buffer.  
  
 **SQLGetData** retornará SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres) quando *BufferLength* é menor que 0 mas não quando *BufferLength* é 0.  
  
 *StrLen_or_IndPtr*  
 [Saída] Ponteiro para o buffer no qual retornar o valor de tamanho ou indicador. Se esse for um ponteiro nulo, nenhum valor de tamanho ou indicador é retornado. Isso retornará um erro quando os dados que estão sendo buscados forem NULL.  
  
 **SQLGetData** pode retornar os seguintes valores no buffer de comprimento/indicador:  
  
-   O comprimento dos dados disponíveis para retornar  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Para obter mais informações, consulte [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) e "Comentários" neste tópico.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetData** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Nem todos os dados da coluna especificada, *Col_or_Param_Num*, pôde ser recuperado em uma única chamada à função. SQL_NO_TOTAL ou o comprimento dos dados restantes da coluna especificada antes da chamada atual para **SQLGetData** é retornado na \* *StrLen_or_IndPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obter mais informações sobre como usar várias chamadas para **SQLGetData** para uma única coluna, consulte "Comentários".|  
|01S07|Truncamento fracionário|Os dados retornados de uma ou mais colunas foi truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para o tempo, carimbo de hora e tipos de dados de intervalo que contém um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pode ser convertido para o tipo de dados C especificado pelo argumento *TargetType*.|  
|07009|Índice de descritor inválido|O valor especificado para o argumento *Col_or_Param_Num* era 0, e o atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *Col_or_Param_Num* era maior que o número de colunas no conjunto de resultados.<br /><br /> O *Col_or_Param_Num* valor não era igual ao ordinal do parâmetro que está disponível.<br /><br /> (DM) da coluna especificada foi associada. Essa descrição não se aplica a drivers de retornam a máscara de bits para a opção SQL_GETDATA_EXTENSIONS na SQL_GD_BOUND **SQLGetInfo**.<br /><br /> (DM) o número da coluna especificado era menor que ou igual ao número da coluna de limite mais alto. Essa descrição não se aplica a drivers de retornam a máscara de bits para a opção SQL_GETDATA_EXTENSIONS na SQL_GD_ANY_COLUMN **SQLGetInfo**.<br /><br /> (DM) o aplicativo já chamou **SQLGetData** para a linha atual; o número da coluna especificada na chamada atual era menor que o número da coluna especificada na chamada anterior; e o driver não retorna o SQL _ Bitmask GD_ANY_ORDER para a opção SQL_GETDATA_EXTENSIONS na **SQLGetInfo**.<br /><br /> (DM) a *TargetType* argumento era SQL_ARD_TYPE e o *Col_or_Param_Num* registro de descritor na descartar falhou a verificação de consistência.<br /><br /> (DM) a *TargetType* argumento era SQL_ARD_TYPE, e o valor no campo SQL_DESC_COUNT da descartar era menor do que o *Col_or_Param_Num* argumento.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22002|Variável de indicador necessária, mas não fornecida|*StrLen_or_IndPtr* é um ponteiro nulo e dados nulos foi recuperados.|  
|22003|Valor numérico fora do intervalo|Retornando o valor numérico (como numérico ou cadeia de caracteres) para a coluna teria causado parte inteira (em vez de fracionários) o número a ser truncado.<br /><br /> Para obter mais informações, consulte [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de data/hora inválido|A coluna de caractere no conjunto de resultados foi associada a uma data, hora ou estrutura de carimbo de hora do C e o valor na coluna era uma data inválida, hora ou carimbo de hora, respectivamente. Para obter mais informações, consulte [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|Divisão por zero|Um valor de uma expressão aritmética que resultaram na divisão por zero foi retornado.|  
|22015|Estouro no campo de intervalo|A atribuição de um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao retornar dados para um tipo de intervalo de C, não houve nenhuma representação do valor do tipo SQL no tipo de intervalo de C.|  
|22018|Valor de caractere inválido para especificação de conversão|Uma coluna de caractere no conjunto de resultados foi retornada para um buffer de caracteres C, e a coluna continha um caractere para o qual não havia nenhuma representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo C associado.|  
|24000|Estado de cursor inválido|(DM), a função foi chamada sem primeiro chamar **SQLFetch** ou **SQLFetchScroll** para posicionar o cursor na linha de dados necessários.<br /><br /> (DM) a *StatementHandle* estava em um estado de executado, mas nenhum conjunto de resultados foi associado a *StatementHandle*.<br /><br /> Um cursor foi aberto na *StatementHandle* e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada, mas o cursor é posicionado antes do início do conjunto de resultados ou após o fim do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na *MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY003|Tipo de programa fora do intervalo|(DM) o argumento *TargetType* não era um tipo de dados válidos, SQL_C_DEFAULT, SQL_ARD_TYPE (no caso de recuperação de dados de coluna) ou SQL_APD_TYPE (no caso de recuperação de dados de parâmetro).<br /><br /> (DM) o argumento *Col_or_Param_Num* era 0 e o argumento *TargetType* não estava SQL_C_BOOKMARK para um indicador de comprimento fixo ou SQL_C_VARBOOKMARK por um indicador de comprimento variável.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread e, em seguida, a função foi chamado novamente na *StatementHandle*.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *TargetValuePtr* é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) especificado *StatementHandle* não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetData** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) a *StatementHandle* estava em um estado de executado, mas nenhum conjunto de resultados foi associado a *StatementHandle*.<br /><br /> Uma chamada para **SQLExeceute**, **SQLExecDirect**, ou **SQLMoreResults** retornados SQL_PARAM_DATA_AVAILABLE, mas **SQLGetData** foi chamado , em vez de **SQLParamData**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *BufferLength* foi menor que 0.<br /><br /> O valor especificado para o argumento *BufferLength* era menor do que 4, o *Col_or_Param_Num* argumento foi definido como 0 e o driver foi um ODBC 2 *. x* driver.|  
|HY109|Posição do cursor inválida|O cursor é posicionado (por **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**, ou **SQLBulkOperations**) em uma linha que foi excluída ou não pôde ser buscada.<br /><br /> O cursor foi um cursor de somente avanço e o tamanho do conjunto de linhas foi maior do que um.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não suporta o uso de **SQLGetData** com várias linhas na **SQLFetchScroll**. Essa descrição não se aplica a drivers de retornam a máscara de bits para a opção SQL_GETDATA_EXTENSIONS na SQL_GD_BLOCK **SQLGetInfo**.<br /><br /> A driver ou fonte de dados não suporta a conversão especificada pela combinação da *TargetType* argumento e o tipo de dados SQL da coluna correspondente. Esse erro se aplica somente quando o tipo de dados SQL da coluna foi mapeado para um tipo de dados SQL específica do driver.<br /><br /> O driver dá suporte a apenas o ODBC 2 *. x*e o argumento *TargetType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e qualquer um dos tipos de dados de intervalo C listados na [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice d: Tipos de dados.<br /><br /> O driver dá suporte apenas a versões ODBC anteriores 3,50 e o argumento *TargetType* foi SQL_C_GUID.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) o driver correspondente a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetData** retorna os dados em uma coluna especificada. **SQLGetData** pode ser chamado somente depois que uma ou mais linhas foram buscadas do conjunto de resultados por **SQLFetch**, **SQLFetchScroll**, ou **SQLExtendedFetch**. Se os dados de comprimento variável são muito grandes para ser retornado em uma única chamada para **SQLGetData** (devido a uma limitação no aplicativo), **SQLGetData** pode recuperá-lo em partes. É possível associar algumas colunas em uma linha e a chamada **SQLGetData** para outros, embora isso seja sujeito a algumas restrições. Para obter mais informações, consulte [Obtendo dados Long](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Para obter informações sobre como usar **SQLGetData** com os parâmetros de saída em fluxo, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Usando o SQLGetData  
 Se o driver não dá suporte a extensões a serem **SQLGetData**, a função pode retornar dados somente para colunas não associadas com um número maior do que da última coluna associada. Além disso, dentro de uma linha de dados, o valor de *Col_or_Param_Num* argumento em cada chamada para **SQLGetData** deve ser maior que ou igual ao valor de *Col_or_Param_Num*na chamada anterior; ou seja, os dados devem ser recuperados em ordem de número de coluna crescente. Por fim, se nenhuma extensão têm suporte, **SQLGetData** não pode ser chamado se o tamanho do conjunto de linhas for maior que 1.  
  
 Drivers podem relaxar com alguma dessas restrições. Para determinar quais restrições alivia um driver, um aplicativo chama **SQLGetInfo** com qualquer uma das seguintes opções SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** pode ser chamado para retornar valores de parâmetro de saída. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Se essa opção for retornada, **SQLGetData** podem ser chamados para qualquer coluna não associada, incluindo aqueles antes da última coluna associada.  
  
-   SQL_GD_ANY_ORDER. Se essa opção for retornada, **SQLGetData** pode ser chamado para colunas não associadas em qualquer ordem.  
  
-   SQL_GD_BLOCK. Se essa opção for retornada pela **SQLGetInfo** para o tipo de informação SQL_GETDATA_EXTENSIONS, o driver dá suporte a chamadas para **SQLGetData** quando o tamanho do conjunto de linhas for maior que 1 e o aplicativo pode chamar **SQLSetPos** com a opção SQL_POSITION para posicionar o cursor na linha correta antes de chamar **SQLGetData.**  
  
-   SQL_GD_BOUND. Se essa opção for retornada, **SQLGetData** pode ser chamado para colunas associadas, bem como dessas colunas.  
  
 Há duas exceções a essas restrições e a capacidade de um driver de relaxá-los. Primeiro, **SQLGetData** nunca deve ser chamado para um cursor de avanço e somente quando o tamanho do conjunto de linhas for maior que 1. Em segundo lugar, se um driver dá suporte a indicadores, ele sempre deve suportar a capacidade de chamar **SQLGetData** para a coluna 0, mesmo se ele não permite que aplicativos chamem **SQLGetData** para outras colunas antes que a última coluna associada. (Quando um aplicativo está funcionando com um ODBC 2 *. x* driver **SQLGetData** retornará com êxito um indicador, quando chamado com *Col_or_Param_Num* igual a 0 após uma chamada para **SQLFetch**, porque **SQLFetch** é mapeado por ODBC 3 *. x* para o Gerenciador de Driver **SQLExtendedFetch** com um  *FetchOrientation* de SQL_FETCH_NEXT, e **SQLGetData** com um *Col_or_Param_Num* 0 é mapeado por ODBC 3 *. x* para o Gerenciador de Driver **SQLGetStmtOption** com um *fOption* de SQL_GET_BOOKMARK.)  
  
 **SQLGetData** não pode ser usado para recuperar o indicador de uma linha recém-inserida chamando **SQLBulkOperations** com a opção SQL_ADD, porque o cursor não está posicionado na linha. Um aplicativo pode recuperar o indicador para esse tipo de linha de associação a coluna 0 antes de chamar **SQLBulkOperations** com SQL_ADD, caso em que **SQLBulkOperations** retorna o indicador no buffer de associado. **SQLFetchScroll** , em seguida, pode ser chamado com SQL_FETCH_BOOKMARK para reposicionar o cursor na linha.  
  
 Se o *TargetType* argumento é um tipo de dados de intervalo, a precisão de à esquerda do intervalo de padrão (2) e a precisão de segundos de intervalo padrão (6), conforme definido nos campos de SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION Descartar, respectivamente, são usados para os dados. Se o *TargetType* argumento é um tipo de dados SQL_C_NUMERIC, a precisão padrão (definido pelo driver) e padrão de escala (0), conforme definido nos campos de SQL_DESC_PRECISION e SQL_DESC_SCALE a descartar, é usado para os dados. Se qualquer escala ou precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo de descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**. Ele pode definir o campo SQL_DESC_CONCISE_TYPE como SQL_C_NUMERIC e chame **SQLGetData** com um *TargetType* argumento de SQL_ARD_TYPE, que fará com que os valores de precisão e escala nos campos de descritor a ser usado.  
  
> [!NOTE]
>  No ODBC 2 *. x*, o conjunto de aplicativos *TargetType* SQL_C_DATE, SQL_C_TIME ou SQL_C_TIMESTAMP para indicar que \* *TargetValuePtr* for uma data, hora, ou estrutura de carimbo de hora. Em ODBC 3 *. x*, o conjunto de aplicativos *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME ou SQL_C_TYPE_TIMESTAMP. O Gerenciador de Driver faz mapeamentos apropriados se necessário, com base na versão do aplicativo e o driver.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recuperando dados de comprimento variável em partes  
 **SQLGetData** pode ser usado para recuperar dados de uma coluna que contém os dados de comprimento variável em partes - ou seja, quando o identificador do tipo de dados SQL da coluna é SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL _ WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY ou um identificador específico do driver para um tipo de comprimento variável.  
  
 Para recuperar dados de uma coluna em partes, o aplicativo chama **SQLGetData** várias vezes sucessivamente para a mesma coluna. Em cada chamada **SQLGetData** retorna a próxima parte dos dados. É até o aplicativo para a remontagem de partes, tomando cuidado para remover o caractere nulo de terminação de partes intermediários de dados de caracteres. Se houver mais dados para retornar ou não buffer suficiente foi alocado para o caractere de terminação **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dados truncados). Quando ele retorna a última parte dos dados, **SQLGetData** retorna SQL_SUCCESS. Nem SQL_NO_TOTAL nem zero pode ser retornado na última chamada válida para recuperar dados de uma coluna, pois o aplicativo, em seguida, teria que não há como saber quanto dos dados no buffer de aplicativo é válido. Se **SQLGetData** é chamado depois disso, ele retornar SQL_NO_DATA. Para obter mais informações, consulte a próxima seção, "Recuperando dados com o SQLGetData."  
  
 Indicadores de comprimento variável podem ser retornados em partes por **SQLGetData**. Assim como acontece com outros dados, uma chamada para **SQLGetData** para retornar os indicadores de comprimento variável em partes retornará SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita) e SQL_SUCCESS_WITH_INFO quando há mais dados a serem retornados. Isso é diferente do que o caso quando um indicador de comprimento variável será truncado por uma chamada para **SQLFetch** ou **SQLFetchScroll**, que retorna SQL_ERROR e SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
 **SQLGetData** não pode ser usado para retornar dados de comprimento fixo em partes. Se **SQLGetData** é chamado mais de uma vez em uma linha para uma coluna que contém dados de comprimento fixo, ele retornar SQL_NO_DATA para todas as chamadas após o primeiro.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperando parâmetros de saída em fluxo  
 Se um driver compatível com os parâmetros de saída em fluxo, um aplicativo pode chamar **SQLGetData** com um pequeno do buffer várias vezes para recuperar um valor de parâmetro grande. Para obter mais informações sobre o parâmetro de saída em fluxo, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recuperando dados com o SQLGetData  
 Para retornar dados para a coluna especificada, **SQLGetData** executa a seguinte sequência de etapas:  
  
1.  Retorna SQL_NO_DATA se já tiver retornado todos os dados da coluna.  
  
2.  Conjuntos \* *StrLen_or_IndPtr* como SQL_NULL_DATA se os dados forem NULL. Se os dados forem NULL e *StrLen_or_IndPtr* é um ponteiro nulo, **SQLGetData** retornará SQLSTATE 22002 (variável de indicador necessária, mas não fornecida).  
  
     Se os dados para a coluna não for nulos, **SQLGetData** prossegue para a etapa 3.  
  
3.  Se o atributo da instrução SQL_ATTR_MAX_LENGTH é definido como um valor diferente de zero, se a coluna contiver caracteres ou dados binários e se **SQLGetData** não foi chamado anteriormente para a coluna, os dados são truncados para SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  O atributo da instrução SQL_ATTR_MAX_LENGTH destina-se para reduzir o tráfego de rede. Ele geralmente é implementado pela fonte de dados, que trunca os dados antes de retorná-lo em toda a rede. Drivers e fontes de dados não são necessários para dar suporte a ele. Portanto, para garantir que os dados são truncados para um tamanho específico, um aplicativo deve alocar um buffer desse tamanho e especifique o tamanho na *BufferLength* argumento.  
  
4.  Converte os dados para o tipo especificado na *TargetType*. Os dados são fornecidos a precisão e escala padrão para esse tipo de dados. Se *TargetType* é SQL_ARD_TYPE, os dados de tipo no campo SQL_DESC_CONCISE_TYPE da descartar é usado. Se *TargetType* é SQL_ARD_TYPE, os dados são fornecidos a precisão e escala em SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, e digitar o SQL_DESC_CONCISE campos SQL_DESC_SCALE de descartar, dependendo dos dados Campo de tipo de _. Se qualquer escala ou precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo de descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
5.  Se os dados foi convertidos em um tipo de dados de comprimento variável, como caractere ou binário, **SQLGetData** verifica se o comprimento dos dados excede *BufferLength*. Se o comprimento dos dados de caractere (incluindo o caractere nulo de terminação) ultrapassar *BufferLength*, **SQLGetData** trunca os dados a serem *BufferLength* menos o comprimento de um caractere nulo de terminação. Ele, em seguida, termina em nulo os dados. Se o comprimento dos dados binários excede o comprimento de buffer de dados, **SQLGetData** trunca a *BufferLength* bytes.  
  
     Se o buffer de dados fornecido é muito pequeno para conter o caractere de terminação null, **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01004.  
  
     **SQLGetData** nunca trunca os dados convertidos para dados de comprimento fixo de tipos; ele sempre pressupõe que o comprimento de **TargetValuePtr* é o tamanho do tipo de dados.  
  
6.  Coloca os dados convertidos (e possivelmente truncados) no \* *TargetValuePtr*. Observe que **SQLGetData** não podem retornar dados fora de linha.  
  
7.  Coloca o comprimento dos dados no \* *StrLen_or_IndPtr*. Se *StrLen_or_IndPtr* é um ponteiro nulo, **SQLGetData** não retorna o comprimento.  
  
    -   Para caracteres ou dados binários, esse é o comprimento dos dados após a conversão e antes do truncamento devido à *BufferLength*. Se o driver não puder determinar o comprimento dos dados após a conversão, como, às vezes, é o caso com dados longos, ele retornará SQL_SUCCESS_WITH_INFO e define o comprimento para SQL_NO_TOTAL. (A última chamada para **SQLGetData** devem sempre retornar o comprimento dos dados, e não em zero ou SQL_NO_TOTAL.) Se os dados foram truncados devido ao atributo de instrução SQL_ATTR_MAX_LENGTH, o valor desse atributo - em vez do comprimento real - é colocado no \* *StrLen_or_IndPtr*. Isso ocorre porque esse atributo foi projetado para truncar os dados no servidor antes da conversão, portanto, o driver não tem nenhuma maneira de descobrir o que o comprimento real é. Quando **SQLGetData** é chamado várias vezes sucessivamente para a mesma coluna, esse é o comprimento dos dados disponíveis no início da chamada atual; ou seja, o tamanho diminui com cada chamada subsequente.  
  
    -   Para todos os outros tipos de dados, isso é o comprimento dos dados após a conversão; ou seja, ele é o tamanho do tipo ao qual os dados foi convertidos.  
  
8.  Se os dados são truncados sem perda de significância durante a conversão (por exemplo, o número real 1,234 será truncado quando convertido para o inteiro 1) ou porque *BufferLength* é muito pequeno (por exemplo, a cadeia de caracteres "abcdef" é colocada em um buffer de 4 bytes), **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e o SQLSTATE 01004 (dados truncados). Se os dados são truncados sem perda de significância devido ao atributo de instrução de SQL_ATTR_MAX_LENGTH **SQLGetData** retorna SQL_SUCCESS e não retornará SQLSTATE 01004 (dados truncados).  
  
 O conteúdo do buffer de dados associado (se **SQLGetData** é chamado em uma coluna associada) e o buffer de comprimento/indicador são indefinidos se **SQLGetData** não retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
 Chamadas sucessivas à **SQLGetData** recuperará os dados da última coluna solicitada; deslocamentos anteriores se tornarão inválidos. Por exemplo, quando a sequência a seguir é executada:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 a segunda chamada para SQLGetData(icol=n) recupera dados desde o início da coluna n. Qualquer deslocamento dos dados devido a chamadas anteriores ao **SQLGetData** para a coluna não é válida.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descritores e SQLGetData  
 **SQLGetData** não interage diretamente com os campos do descritor.  
  
 Se *TargetType* é SQL_ARD_TYPE, os dados de tipo no campo SQL_DESC_CONCISE_TYPE da descartar é usado. Se *TargetType* é SQL_ARD_TYPE ou SQL_C_DEFAULT, os dados são fornecidos a precisão e escala em SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, e SQL_DESC_SCALE campos de descartar, dependendo dos dados de tipo no campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa uma **selecionar** instrução para retornar um conjunto de resultados do cliente IDs, nomes e classificados por nome, a ID e o número de telefone de números de telefone. Para cada linha de dados, ele chama **SQLFetch** para posicionar o cursor para a próxima linha. Ele chama **SQLGetData** para recuperar os dados buscados; os buffers para os dados e o número de bytes retornado são especificados na chamada para **SQLGetData**. Por fim, imprime o nome de cada funcionário, ID e número de telefone.  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Atribuindo armazenamento para uma coluna em um conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações em massa que não estão relacionados à posição do bloco de cursor|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executar uma instrução SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha de dados ou um bloco de dados em uma direção de somente avanço|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Enviar dados de parâmetro em tempo de execução|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posicionando o cursor, a atualização de dados no conjunto de linhas, ou a atualização ou exclusão de dados no conjunto de linhas|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
