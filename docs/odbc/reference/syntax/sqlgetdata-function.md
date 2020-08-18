---
description: Função SQLGetData
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a659e1bb5ad7765dbfcbcb01dbc16744de7cfc20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461074"
---
# <a name="sqlgetdata-function"></a>Função SQLGetData
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLGetData** recupera dados para uma única coluna no conjunto de resultados ou para um único parâmetro depois que **SQLParamData** retorna SQL_PARAM_DATA_AVAILABLE. Ele pode ser chamado várias vezes para recuperar dados de comprimento variável em partes.  
  
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
 Entrada Identificador de instrução.  
  
 *Col_or_Param_Num*  
 Entrada Para recuperar dados de coluna, é o número da coluna para a qual retornar dados. As colunas do conjunto de resultados são numeradas no aumento da ordem das colunas, começando em 1. A coluna de indicadores é o número da coluna 0; Isso pode ser especificado somente se os indicadores estiverem habilitados.  
  
 Para recuperar dados de parâmetro, é o ordinal do parâmetro, que começa em 1.  
  
 *TargetType*  
 Entrada O identificador de tipo do tipo de dados C do buffer **TargetValuePtr* . Para obter uma lista de tipos de dados C válidos e identificadores de tipo, consulte a seção [tipos de dados c](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice D: tipos de dados.  
  
 Se *TargetType* for SQL_ARD_TYPE, o driver usará o identificador de tipo especificado no campo SQL_DESC_CONCISE_TYPE do ARD. Se *TargetType* for SQL_APD_TYPE, **SQLGetData** usará o mesmo tipo de dados C que foi especificado em **SQLBindParameter**. Caso contrário, o tipo de dados C especificado em **SQLGetData** substituirá o tipo de dados c especificado em **SQLBindParameter**. Se for SQL_C_DEFAULT, o driver selecionará o tipo de dados C padrão com base no tipo de dados SQL da origem.  
  
 Você também pode especificar um tipo de dados C estendido. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 Der Ponteiro para o buffer no qual os dados são retornados.  
  
 *TargetValuePtr* não pode ser nulo.  
  
 *BufferLength*  
 Entrada Comprimento do buffer **TargetValuePtr* em bytes.  
  
 O driver usa *BufferLength* para evitar a gravação após o final do \* buffer *TargetValuePtr* ao retornar dados de comprimento variável, como caracteres ou dados binários. Observe que o driver conta o caractere de terminação nula ao retornar dados de caractere para \* *TargetValuePtr*. *O *TargetValuePtr* deve, portanto, conter espaço para o caractere de terminação nula ou o driver truncará os dados.  
  
 Quando o driver retorna dados de comprimento fixo, como um inteiro ou uma estrutura de data, o driver ignora *BufferLength* e assume que o buffer é grande o suficiente para manter os dados. Portanto, é importante que o aplicativo aloque um buffer grande o suficiente para dados de comprimento fixo ou o driver será gravado após o final do buffer.  
  
 **SQLGetData** retorna SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido) quando *BufferLength* é menor que 0, mas não quando *BufferLength* é 0.  
  
 *StrLen_or_IndPtr*  
 Der Ponteiro para o buffer no qual retornar o comprimento ou o valor do indicador. Se esse for um ponteiro nulo, nenhum valor de comprimento ou indicador será retornado. Isso retorna um erro quando os dados que estão sendo buscados são nulos.  
  
 **SQLGetData** pode retornar os seguintes valores no buffer de comprimento/indicador:  
  
-   O comprimento dos dados disponíveis para retornar  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Para obter mais informações, consulte [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) e "Comentários" neste tópico.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetData** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Nem todos os dados para a coluna especificada, *Col_or_Param_Num*, poderiam ser recuperados em uma única chamada para a função. SQL_NO_TOTAL ou o comprimento dos dados restantes na coluna especificada antes da chamada atual para **SQLGetData** é retornado em \* *StrLen_or_IndPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obter mais informações sobre como usar várias chamadas para **SQLGetData** para uma única coluna, consulte "Comentários".|  
|01S07|Truncamento fracionário|Os dados retornados para uma ou mais colunas foram truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para os tipos de dados time, timestamp e Interval que contêm um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pode ser convertido para o tipo de dados C especificado pelo argumento *TargetType*.|  
|07009|Índice de descritor inválido|O valor especificado para o argumento *Col_or_Param_Num* era 0 e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *Col_or_Param_Num* foi maior que o número de colunas no conjunto de resultados.<br /><br /> O valor de *Col_or_Param_Num* não era igual ao ordinal do parâmetro que está disponível.<br /><br /> (DM) a coluna especificada foi associada. Essa descrição não se aplica a drivers que retornam o bitmask SQL_GD_BOUND para a opção SQL_GETDATA_EXTENSIONS em **SQLGetInfo**.<br /><br /> (DM) o número da coluna especificada era menor ou igual ao número da coluna associada mais alta. Essa descrição não se aplica a drivers que retornam o bitmask SQL_GD_ANY_COLUMN para a opção SQL_GETDATA_EXTENSIONS em **SQLGetInfo**.<br /><br /> (DM) o aplicativo já chamou **SQLGetData** para a linha atual; o número da coluna especificada na chamada atual era menor que o número da coluna especificada na chamada anterior; e o driver não retorna o SQL_GD_ANY_ORDER bitmask para a opção SQL_GETDATA_EXTENSIONS em **SQLGetInfo**.<br /><br /> (DM) o argumento *TargetType* foi SQL_ARD_TYPE e o registro do descritor de *Col_or_Param_Num* no ARD falhou na verificação de consistência.<br /><br /> (DM) o argumento *TargetType* foi SQL_ARD_TYPE e o valor no campo SQL_DESC_COUNT do ARD era menor que o argumento *Col_or_Param_Num* .|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22002|Variável de indicador necessária, mas não fornecida|*StrLen_or_IndPtr* foi um ponteiro nulo e dados nulos foram recuperados.|  
|22003|Valor numérico fora do intervalo|Retornar o valor numérico (como numérico ou cadeia de caracteres) para a coluna teria causado a parte inteira (em oposição à fração) do número a ser truncado.<br /><br /> Para obter mais informações, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de data e hora inválido|A coluna de caracteres no conjunto de resultados foi associada a uma estrutura C data, hora ou timestamp, e o valor na coluna era uma data, hora ou carimbo de hora inválido, respectivamente. Para obter mais informações, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|Divisão por zero|Um valor de uma expressão aritmética que resultou em divisão por zero foi retornado.|  
|22015|Estouro no campo de intervalo|A atribuição de um tipo de SQL numérico ou de intervalo exato para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao retornar dados para um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.|  
|22018|Valor de caractere inválido para especificação de conversão|Uma coluna de caracteres no conjunto de resultados foi retornada para um buffer de caractere C e a coluna continha um caractere para o qual não havia nenhuma representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo associado de C.|  
|24.000|Estado de cursor inválido|(DM) a função foi chamada sem primeiro chamar **SQLFetch** ou **SQLFetchScroll** para posicionar o cursor na linha de dados necessária.<br /><br /> (DM) o *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.<br /><br /> Um cursor estava aberto no *StatementHandle* e **SQLFetch** ou **SQLFetchScroll** foi chamado, mas o cursor foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer *MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY003|Tipo de programa fora do intervalo|(DM) o argumento *TargetType* não era um tipo de dados válido, SQL_C_DEFAULT SQL_ARD_TYPE (no caso de recuperação de dados de coluna) ou SQL_APD_TYPE (no caso de recuperação de dados de parâmetro).<br /><br /> (DM) o argumento *Col_or_Param_Num* era 0 e o argumento *TargetType* não foi SQL_C_BOOKMARK para um indicador de comprimento fixo ou SQL_C_VARBOOKMARK para um indicador de comprimento variável.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado em *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread e, em seguida, a função foi chamada novamente no *StatementHandle*.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *TargetValuePtr* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) o *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLGetData** foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) o *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.<br /><br /> Uma chamada para **SQLExeceute**, **SQLExecDirect**ou **SQLMoreResults** retornou SQL_PARAM_DATA_AVAILABLE, mas **SQLGetData** foi chamado, em vez de **SQLParamData**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *BufferLength* era menor que 0.<br /><br /> O valor especificado para o argumento *BufferLength* era menor que 4, o argumento *Col_or_Param_Num* foi definido como 0 e o driver era um driver ODBC 2 *. x* .|  
|HY109|Posição do cursor inválida|O cursor foi posicionado (por **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**ou **SQLBulkOperations**) em uma linha que foi excluída ou não pôde ser buscada.<br /><br /> O cursor era um cursor de somente avanço e o tamanho do conjunto de linhas era maior que um.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não dá suporte ao uso de **SQLGetData** com várias linhas em **SQLFetchScroll**. Essa descrição não se aplica a drivers que retornam o bitmask SQL_GD_BLOCK para a opção SQL_GETDATA_EXTENSIONS em **SQLGetInfo**.<br /><br /> O driver ou a fonte de dados não oferece suporte à conversão especificada pela combinação do argumento *TargetType* e do tipo de dados SQL da coluna correspondente. Esse erro se aplica somente quando o tipo de dados SQL da coluna foi mapeado para um tipo de dados SQL específico de driver.<br /><br /> O driver dá suporte apenas ao ODBC 2 *. x*, e o argumento *TargetType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e qualquer um dos tipos de dados do intervalo C listados em [tipos de dados c](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice D: tipos de dados.<br /><br /> O driver só dá suporte a versões ODBC anteriores a 3,50, e o argumento *TargetType* foi SQL_C_GUID.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver correspondente ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetData** retorna os dados em uma coluna especificada. **SQLGetData** pode ser chamado somente depois que uma ou mais linhas forem buscadas do conjunto de resultados por **SQLFetch**, **SQLFetchScroll**ou **SQLExtendedFetch**. Se os dados de comprimento variável forem muito grandes para serem retornados em uma única chamada para **SQLGetData** (devido a uma limitação no aplicativo), o **SQLGetData** poderá recuperá-lo em partes. É possível associar algumas colunas em uma linha e chamar **SQLGetData** para outras, embora isso esteja sujeito a algumas restrições. Para obter mais informações, consulte [obtendo dados longos](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Para obter informações sobre como usar **SQLGetData** com parâmetros de saída em fluxo, consulte [recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Usando SQLGetData  
 Se o driver não oferecer suporte a extensões para **SQLGetData**, a função poderá retornar dados somente para colunas não associadas com um número maior que o da última coluna associada. Além disso, dentro de uma linha de dados, o valor do argumento *Col_or_Param_Num* em cada chamada para **SQLGetData** deve ser maior ou igual ao valor de *Col_or_Param_Num* na chamada anterior; ou seja, os dados devem ser recuperados em ordem crescente de números de coluna. Por fim, se não houver suporte para nenhuma extensão, **SQLGetData** não poderá ser chamado se o tamanho do conjunto de linhas for maior que 1.  
  
 Os drivers podem relaxar com qualquer uma dessas restrições. Para determinar quais restrições um driver ameniza, um aplicativo chama **SQLGetInfo** com qualquer uma das seguintes opções de SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** pode ser chamado para retornar valores de parâmetro de saída. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Se essa opção for retornada, **SQLGetData** poderá ser chamado para qualquer coluna desassociada, incluindo aquelas antes da última coluna associada.  
  
-   SQL_GD_ANY_ORDER. Se essa opção for retornada, **SQLGetData** poderá ser chamado para colunas desassociadas em qualquer ordem.  
  
-   SQL_GD_BLOCK. Se essa opção for retornada por **SQLGetInfo** para o SQL_GETDATA_EXTENSIONS InfoType, o driver dará suporte a chamadas para **SQLGetData** quando o tamanho do conjunto de linhas for maior que 1 e o aplicativo puder chamar **SQLSetPos** com a opção SQL_POSITION para posicionar o cursor na linha correta antes de chamar **SQLGetData.**  
  
-   SQL_GD_BOUND. Se essa opção for retornada, **SQLGetData** poderá ser chamado para colunas associadas, bem como colunas desassociadas.  
  
 Há duas exceções a essas restrições e a capacidade de um driver de relaxar. Primeiro, **SQLGetData** nunca deve ser chamado para um cursor de somente avanço quando o tamanho do conjunto de linhas for maior que 1. Em segundo lugar, se um driver oferecer suporte a indicadores, ele sempre deve oferecer suporte à capacidade de chamar **SQLGetData** para a coluna 0, mesmo que não permita que os aplicativos chamem **SQLGetData** para outras colunas antes da última coluna associada. (Quando um aplicativo estiver funcionando com um ODBC 2 *. x* Driver, **SQLGetData** retornará com êxito um indicador quando chamado com *Col_or_Param_Num* igual a 0 após uma chamada para **SQLFetch**, porque **SQLFetch** é mapeado pelo Gerenciador de driver ODBC*3. x* para **SQLExtendedFetch** com *FetchOrientation* de SQL_FETCH_NEXT e **SQLGetData** com um *Col_or_Param_Num* de 0 é mapeado pelo Gerenciador de driver ODBC 3 *. x* para **SQLGetStmtOption** com um *fOption* de SQL_GET_BOOKMARK.)  
  
 **SQLGetData** não pode ser usado para recuperar o indicador de uma linha que acabou de ser inserida chamando **SQLBulkOperations** com a opção SQL_ADD, porque o cursor não está posicionado na linha. Um aplicativo pode recuperar o indicador para tal linha ligando a coluna 0 antes de chamar **SQLBulkOperations** com SQL_ADD; nesse caso, **SQLBulkOperations** retorna o indicador no buffer associado. **SQLFetchScroll** pode ser chamado com SQL_FETCH_BOOKMARK para reposicionar o cursor nessa linha.  
  
 Se o argumento *TargetType* for um tipo de dados de intervalo, a precisão inicial do intervalo padrão (2) e a precisão do intervalo padrão de segundos (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION de ARD, respectivamente, serão usados para os dados. Se o argumento *TargetType* for um tipo de dados SQL_C_NUMERIC, a precisão padrão (definida pelo driver) e a escala padrão (0), conforme definido nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, serão usados para os dados. Se qualquer precisão ou escala padrão não for apropriada, o aplicativo deverá definir explicitamente o campo de descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**. Ele pode definir o campo SQL_DESC_CONCISE_TYPE como SQL_C_NUMERIC e chamar **SQLGetData** com um argumento *TargetType* de SQL_ARD_TYPE, o que fará com que os valores de precisão e escala nos campos do descritor sejam usados.  
  
> [!NOTE]
>  No ODBC 2 *. x*, os aplicativos definem *TargetType* como SQL_C_DATE, SQL_C_TIME ou SQL_C_TIMESTAMP para indicar que \* *TargetValuePtr* é uma estrutura de data, hora ou timestamp. No ODBC 3 *. x*, os aplicativos definem *TargetType* como SQL_C_TYPE_DATE, SQL_C_TYPE_TIME ou SQL_C_TYPE_TIMESTAMP. O Gerenciador de driver faz mapeamentos apropriados, se necessário, com base na versão do aplicativo e do driver.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recuperando dados de comprimento variável em partes  
 **SQLGetData** pode ser usado para recuperar dados de uma coluna que contém dados de comprimento variável em partes – ou seja, quando o identificador do tipo de dados SQL da coluna é SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY ou um identificador específico de driver para um tipo de comprimento variável.  
  
 Para recuperar dados de uma coluna em partes, o aplicativo chama **SQLGetData** várias vezes em sucessão para a mesma coluna. Em cada chamada, **SQLGetData** retorna a próxima parte dos dados. Cabe ao aplicativo remontar as partes, tomando o cuidado de remover o caractere de terminação nula das partes intermediárias dos dados de caractere. Se houver mais dados a serem retornados ou se não houver buffer suficiente alocado para o caractere de terminação, **SQLGetData** retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dados truncados). Quando ele retorna a última parte dos dados, **SQLGetData** retorna SQL_SUCCESS. Nem SQL_NO_TOTAL nem zero podem ser retornados na última chamada válida para recuperar dados de uma coluna, porque o aplicativo não teria como saber a quantidade de dados no buffer de aplicativo válida. Se **SQLGetData** for chamado depois disso, ele retornará SQL_NO_DATA. Para obter mais informações, consulte a próxima seção, "recuperando dados com SQLGetData".  
  
 Os indicadores de comprimento variável podem ser retornados em partes por **SQLGetData**. Assim como ocorre com outros dados, uma chamada para **SQLGetData** para retornar indicadores de comprimento variável em partes retornará SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita) e SQL_SUCCESS_WITH_INFO quando houver mais dados a serem retornados. Isso é diferente do caso quando um indicador de comprimento variável é truncado por uma chamada para **SQLFetch** ou **SQLFetchScroll**, que retorna SQL_ERROR e SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
 **SQLGetData** não pode ser usado para retornar dados de comprimento fixo em partes. Se **SQLGetData** for chamado mais de uma vez em uma linha para uma coluna que contém dados de comprimento fixo, ele retornará SQL_NO_DATA para todas as chamadas após o primeiro.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperando parâmetros de saída em fluxo  
 Se um driver oferecer suporte a parâmetros de saída em fluxo, um aplicativo poderá chamar **SQLGetData** com um buffer pequeno muitas vezes para recuperar um valor de parâmetro grande. Para obter mais informações sobre o parâmetro de saída em fluxo, consulte [recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recuperando dados com SQLGetData  
 Para retornar dados para a coluna especificada, **SQLGetData** executa a seguinte sequência de etapas:  
  
1.  Retornará SQL_NO_DATA se já tiver retornado todos os dados para a coluna.  
  
2.  Define \* *StrLen_or_IndPtr* como SQL_NULL_DATA se os dados forem nulos. Se os dados forem nulos e *StrLen_or_IndPtr* for um ponteiro nulo, **SQLGetData** retornará SQLSTATE 22002 (variável de indicador necessária, mas não fornecida).  
  
     Se os dados da coluna não forem nulos, **SQLGetData** prosseguirá para a etapa 3.  
  
3.  Se o atributo da instrução SQL_ATTR_MAX_LENGTH for definido como um valor diferente de zero, se a coluna contiver dados de caractere ou binários e, se **SQLGetData** não tiver sido chamado anteriormente para a coluna, os dados serão truncados para SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  O atributo da instrução SQL_ATTR_MAX_LENGTH destina-se a reduzir o tráfego de rede. Geralmente, ele é implementado pela fonte de dados, o que trunca os dados antes de retorná-los pela rede. Os drivers e as fontes de dados não são necessários para dar suporte a ele. Portanto, para garantir que os dados sejam truncados para um tamanho específico, um aplicativo deve alocar um buffer desse tamanho e especificar o tamanho no argumento *BufferLength* .  
  
4.  Converte os dados para o tipo especificado em *TargetType*. Os dados recebem a precisão e a escala padrão para esse tipo de dados. Se *TargetType* for SQL_ARD_TYPE, o tipo de dados no campo SQL_DESC_CONCISE_TYPE do ARD será usado. Se *TargetType* for SQL_ARD_TYPE, os dados receberão a precisão e a escala nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, dependendo do tipo de dados no campo SQL_DESC_CONCISE_TYPE. Se qualquer precisão ou escala padrão não for apropriada, o aplicativo deverá definir explicitamente o campo de descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
5.  Se os dados foram convertidos em um tipo de dados de comprimento variável, como Character ou Binary, **SQLGetData** verifica se o comprimento dos dados excede *BufferLength*. Se o comprimento dos dados de caracteres (incluindo o caractere de terminação nula) exceder *BufferLength*, **SQLGetData** truncará os dados para *BufferLength* menos o comprimento de um caractere de terminação nula. Em seguida, NULL – encerra os dados. Se o comprimento dos dados binários exceder o comprimento do buffer de dados, **SQLGetData** o truncará para *BufferLength* bytes.  
  
     Se o buffer de dados fornecido for muito pequeno para conter o caractere de terminação nula, **SQLGetData** retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01004.  
  
     **SQLGetData** nunca trunca os dados convertidos em tipos de dados de comprimento fixo; Ele sempre pressupõe que o comprimento de **TargetValuePtr* é o tamanho do tipo de dados.  
  
6.  Coloca os dados convertidos (e possivelmente truncados) em \* *TargetValuePtr*. Observe que **SQLGetData** não pode retornar dados fora de linha.  
  
7.  Coloca o comprimento dos dados em \* *StrLen_or_IndPtr*. Se *StrLen_or_IndPtr* era um ponteiro nulo, **SQLGetData** não retornará o comprimento.  
  
    -   Para dados de caracteres ou binários, esse é o comprimento dos dados após a conversão e antes do truncamento devido a *BufferLength*. Se o driver não puder determinar o comprimento dos dados após a conversão, como às vezes é o caso com dados longos, ele retornará SQL_SUCCESS_WITH_INFO e definirá o comprimento como SQL_NO_TOTAL. (A última chamada para **SQLGetData** deve sempre retornar o comprimento dos dados, não zero ou SQL_NO_TOTAL.) Se os dados foram truncados devido ao atributo de instrução SQL_ATTR_MAX_LENGTH, o valor desse atributo, em oposição ao comprimento real, é colocado em \* *StrLen_or_IndPtr*. Isso ocorre porque esse atributo é projetado para truncar dados no servidor antes da conversão, portanto, o driver não tem como descobrir qual é o comprimento real. Quando **SQLGetData** é chamado várias vezes em sucessão para a mesma coluna, esse é o comprimento dos dados disponíveis no início da chamada atual; ou seja, o comprimento diminui em cada chamada subsequente.  
  
    -   Para todos os outros tipos de dados, esse é o comprimento dos dados após a conversão; ou seja, é o tamanho do tipo para o qual os dados foram convertidos.  
  
8.  Se os dados estiverem truncados sem perda de significância durante a conversão (por exemplo, o número real 1,234 é truncado quando convertido no inteiro 1) ou porque *BufferLength* é muito pequeno (por exemplo, a cadeia de caracteres "abcdef" é colocada em um buffer de 4 bytes), **SQLGetData** retorna SQLSTATE 01004 (dados truncados) e SQL_SUCCESS_WITH_INFO. Se os dados estiverem truncados sem perda de significância devido ao atributo da instrução SQL_ATTR_MAX_LENGTH, **SQLGetData** retornará SQL_SUCCESS e não retornará SQLSTATE 01004 (dados truncados).  
  
 O conteúdo do buffer de dados associado (se **SQLGetData** for chamado em uma coluna associada) e o buffer de comprimento/indicador não será definido se **SQLGetData** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
 As chamadas sucessivas para **SQLGetData** recuperarão dados da última coluna solicitada; os deslocamentos anteriores se tornam inválidos. Por exemplo, quando a sequência a seguir é executada:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 a segunda chamada para SQLGetData (iCol = n) recupera dados do início da coluna n. Qualquer deslocamento nos dados devido a chamadas anteriores a **SQLGetData** para a coluna não é mais válido.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descritores e SQLGetData  
 **SQLGetData** não interage diretamente com nenhum campo de descritor.  
  
 Se *TargetType* for SQL_ARD_TYPE, o tipo de dados no campo SQL_DESC_CONCISE_TYPE do ARD será usado. Se *TargetType* for SQL_ARD_TYPE ou SQL_C_DEFAULT, os dados receberão a precisão e a escala nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, dependendo do tipo de dados no campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa uma instrução **Select** para retornar um conjunto de resultados das IDs de cliente, nomes e números de telefone classificados por nome, ID e número de telefone. Para cada linha de dados, ele chama **SQLFetch** para posicionar o cursor para a próxima linha. Ele chama **SQLGetData** para recuperar os dados buscados; os buffers para os dados e o número retornado de bytes são especificados na chamada para **SQLGetData**. Por fim, ele imprime o nome, a ID e o número de telefone de cada funcionário.  
  
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
|Executando operações em massa que não estão relacionadas à posição do cursor de bloco|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma instrução SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha de dados ou um bloco de dados em uma direção somente de avanço|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Enviando dados de parâmetro em tempo de execução|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posicionando o cursor, atualizando os dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de linhas|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
