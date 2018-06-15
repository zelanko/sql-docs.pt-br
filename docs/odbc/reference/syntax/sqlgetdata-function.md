---
title: Função SQLGetData | Microsoft Docs
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
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab603b24536afcbe7304dae907c10ee911d3cfd9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923701"
---
# <a name="sqlgetdata-function"></a>Função SQLGetData
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetData** recupera dados para uma única coluna no conjunto de resultados ou para um único parâmetro após **SQLParamData** retorna SQL_PARAM_DATA_AVAILABLE. Ele pode ser chamado várias vezes para recuperar dados de comprimento variável em partes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Para recuperar dados da coluna, é o número de coluna para a qual retornar dados. Colunas do conjunto de resultados são numeradas em ordem crescente de coluna começando em 1. A coluna de indicador é o número de coluna 0; Isso pode ser especificado somente se os marcadores estão habilitados.  
  
 Para recuperar dados de parâmetro, é o ordinal do parâmetro, que inicia em 1.  
  
 *TargetType*  
 [Entrada] O identificador de tipo do tipo de dados C do **TargetValuePtr* buffer. Para obter uma lista de tipos de dados válidos do C e identificadores de tipo, consulte o [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) seção apêndice d: os tipos de dados.  
  
 Se *TargetType* é SQL_ARD_TYPE, o driver utiliza o identificador de tipo especificado no campo SQL_DESC_CONCISE_TYPE da descartar. Se *TargetType* é SQL_APD_TYPE, **SQLGetData** usará o mesmo tipo de dados C foi especificado em **SQLBindParameter**. Caso contrário, o tipo de dados C é especificado em **SQLGetData** substitui o tipo de dados C especificado em **SQLBindParameter**. Se for SQL_C_DEFAULT, o driver seleciona o tipo de dados C padrão com base no tipo da fonte de dados SQL.  
  
 Você também pode especificar um tipo de dados estendido C. Para obter mais informações, consulte [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Saída] Ponteiro para o buffer no qual retornar os dados.  
  
 *TargetValuePtr* não pode ser NULL.  
  
 *BufferLength*  
 [Entrada] Comprimento do **TargetValuePtr* buffer em bytes.  
  
 O driver usa *BufferLength* para evitar a gravação após o término do \* *TargetValuePtr* buffer ao retornar dados de comprimento variável, como caractere ou dados binários. O driver conta o caractere null de terminação ao retornar dados de caractere para \* *TargetValuePtr*. **TargetValuePtr* , portanto, deve conter um espaço para o caractere null de terminação, ou o driver truncará os dados.  
  
 Quando o driver retorna dados de comprimento fixo, como um número inteiro ou uma estrutura de data, o driver ignorará *BufferLength* e pressupõe que o buffer é grande o suficiente para manter os dados. Portanto, é importante para o aplicativo para alocar um buffer grande o suficiente para dados de comprimento fixo ou o driver irá gravar após o final do buffer.  
  
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
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetData** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Nem todos os dados da coluna especificada, *Col_or_Param_Num*, podem ser recuperados em uma única chamada para a função. SQL_NO_TOTAL ou o comprimento dos dados restantes na coluna especificada antes da chamada atual para **SQLGetData** é retornado no \* *StrLen_or_IndPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obter mais informações sobre como usar várias chamadas para **SQLGetData** para uma única coluna, consulte "Comentários".|  
|01S07|Truncamento fracionário|Os dados retornados de uma ou mais colunas foi truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para o tempo, carimbo de hora e tipos de dados de intervalo que contém um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor dos dados de uma coluna no conjunto de resultados não pode ser convertido para o tipo de dados C especificado pelo argumento *TargetType*.|  
|07009|Índice do descritor inválido|O valor especificado para o argumento *Col_or_Param_Num* 0, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *Col_or_Param_Num* era maior que o número de colunas no conjunto de resultados.<br /><br /> O *Col_or_Param_Num* valor não é igual ao ordinal do parâmetro que está disponível.<br /><br /> (DM) da coluna especificada foi vinculada. Essa descrição não se aplica a drivers de retornam a máscara de bits para a opção SQL_GETDATA_EXTENSIONS SQL_GD_BOUND **SQLGetInfo**.<br /><br /> (DM) o número da coluna especificada era menor ou igual ao número da coluna de limite mais alto. Essa descrição não se aplica a drivers de retornam a máscara de bits para a opção SQL_GETDATA_EXTENSIONS SQL_GD_ANY_COLUMN **SQLGetInfo**.<br /><br /> (DM) o aplicativo já foi chamado **SQLGetData** para a linha atual; o número da coluna especificada na chamada atual era menor do que o número da coluna especificada na chamada anterior; e o driver não retorna o SQL _ GD_ANY_ORDER a máscara de bits para a opção SQL_GETDATA_EXTENSIONS **SQLGetInfo**.<br /><br /> (DM) a *TargetType* argumento era SQL_ARD_TYPE e o *Col_or_Param_Num* registro descritor de descartar falhou a verificação de consistência.<br /><br /> (DM) a *TargetType* argumento SQL_ARD_TYPE, e o valor no campo de SQL_DESC_COUNT a descartar era menor do que o *Col_or_Param_Num* argumento.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22002|Variável de indicador exigida mas não fornecida|*StrLen_or_IndPtr* foi um ponteiro nulo e recuperação de dados NULL.|  
|22003|Valor numérico fora do intervalo|Retornando o valor numérico (como numérico ou cadeia de caracteres) para a coluna teria causado parte inteira (em vez de frações) o número a ser truncado.<br /><br /> Para obter mais informações, consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de datetime inválido|A coluna de caractere no conjunto de resultados foi associada a uma data, hora ou estrutura de carimbo de hora do C e o valor na coluna era uma data inválida, hora ou carimbo de hora, respectivamente. Para obter mais informações, consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|Divisão por zero|Um valor de uma expressão aritmética resultou na divisão por zero foi retornado.|  
|22015|Estouro no campo de intervalo|Atribuição de um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao retornar dados para um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.|  
|22018|Valor de caractere inválido para especificação de coerção|Uma coluna de caractere no conjunto de resultados foi retornada para um buffer de caractere C e a coluna contém um caractere para os quais não houve nenhuma representação no conjunto de caracteres do buffer.<br /><br /> O tipo C foi um numérico exato ou aproximado, uma data e hora ou um tipo de dados do intervalo; o tipo SQL da coluna era de um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo C associado.|  
|24000|Estado de cursor inválido|(DM), a função foi chamada sem primeiro chamar **SQLFetch** ou **SQLFetchScroll** para posicionar o cursor na linha de dados necessários.<br /><br /> (DM) a *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado a *StatementHandle*.<br /><br /> Um cursor foi aberto no *StatementHandle* e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada, mas o cursor é posicionado antes do início do conjunto de resultados ou depois de fim do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no *MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY003|Tipo de programa fora do intervalo|(DM) o argumento *TargetType* não era um tipo de dados válidos, SQL_C_DEFAULT, SQL_ARD_TYPE (no caso de recuperação de dados de coluna) ou SQL_APD_TYPE (no caso de recuperação de dados de parâmetro).<br /><br /> (DM) o argumento *Col_or_Param_Num* era 0 e o argumento *TargetType* não era SQL_C_BOOKMARK para um indicador de comprimento fixo ou SQL_C_VARBOOKMARK para um indicador de comprimento variável.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread e, em seguida, a função foi chamado novamente no *StatementHandle*.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *TargetValuePtr* foi um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) especificado *StatementHandle* não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetData** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) a *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado a *StatementHandle*.<br /><br /> Uma chamada para **SQLExeceute**, **SQLExecDirect**, ou **SQLMoreResults** retornou SQL_PARAM_DATA_AVAILABLE, mas **SQLGetData** foi chamado , em vez de **SQLParamData**.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *BufferLength* era menor do que 0.<br /><br /> O valor especificado para o argumento *BufferLength* era menor que 4, o *Col_or_Param_Num* argumento foi definido como 0 e o driver foi um ODBC 2 *. x* driver.|  
|HY109|Posição de cursor inválido|O cursor é posicionado (por **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**, ou **SQLBulkOperations**) em uma linha que foi excluída ou não pôde ser obtido.<br /><br /> O cursor foi um cursor de somente avanço e o tamanho do conjunto de linhas foi maior que um.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não suporta o uso de **SQLGetData** com várias linhas em **SQLFetchScroll**. Essa descrição não se aplica a drivers de retornam a máscara de bits para a opção SQL_GETDATA_EXTENSIONS SQL_GD_BLOCK **SQLGetInfo**.<br /><br /> A driver ou fonte de dados não suporta a conversão especificada pela combinação da *TargetType* argumento e o tipo de dados SQL da coluna correspondente. Esse erro se aplica somente quando o tipo de dados SQL da coluna foi mapeado para um tipo de dados SQL específico do driver.<br /><br /> O driver dá suporte somente ODBC 2 *. x*e o argumento *TargetType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e qualquer um dos tipos de dados de intervalo C listados na [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice d: os tipos de dados.<br /><br /> O driver só dá suporte a versões ODBC anteriores 3.50 e o argumento *TargetType* foi SQL_C_GUID.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver correspondente a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetData** retorna os dados em uma coluna especificada. **SQLGetData** pode ser chamado somente depois que uma ou mais linhas foram buscadas do conjunto de resultados por **SQLFetch**, **SQLFetchScroll**, ou **SQLExtendedFetch**. Se os dados de comprimento variável são muito grandes para ser retornado em uma única chamada para **SQLGetData** (devido a uma limitação no aplicativo), **SQLGetData** poderá recuperá-lo em partes. É possível associar algumas colunas em uma linha e a chamada **SQLGetData** para outras pessoas, embora isso esteja sujeito a algumas restrições. Para obter mais informações, consulte [Obtendo dados Long](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Para obter informações sobre como usar **SQLGetData** com parâmetros de saída em fluxo, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Usando o SQLGetData  
 Se o driver não dá suporte a extensões de **SQLGetData**, a função pode retornar dados somente para colunas não associadas com um número maior do que a última coluna associada. Além disso, dentro de uma linha de dados, o valor de *Col_or_Param_Num* argumento em cada chamada para **SQLGetData** deve ser maior ou igual ao valor de *Col_or_Param_Num*na chamada anterior; ou seja, os dados devem ser recuperados em ordem de número de coluna crescente. Por fim, não se houver suporte para nenhuma extensão, **SQLGetData** não pode ser chamado se o tamanho do conjunto de linhas for maior que 1.  
  
 Drivers podem relaxar quaisquer dessas restrições. Para determinar quais restrições alivia um driver, um aplicativo chama **SQLGetInfo** com qualquer uma das seguintes opções SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** pode ser chamado para retornar valores de parâmetro de saída. Para obter mais informações, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Se essa opção for retornada, **SQLGetData** pode ser chamado para qualquer coluna desvinculada, incluindo aqueles antes da última coluna associada.  
  
-   SQL_GD_ANY_ORDER. Se essa opção for retornada, **SQLGetData** pode ser chamado para colunas desassociadas em qualquer ordem.  
  
-   SQL_GD_BLOCK. Se essa opção for retornada por **SQLGetInfo** para o tipo de informação de SQL_GETDATA_EXTENSIONS, o driver dá suporte a chamadas para **SQLGetData** quando o tamanho do conjunto de linhas é maior que 1 e o aplicativo pode chamar **SQLSetPos** com a opção SQL_POSITION para posicionar o cursor na linha correta antes de chamar **SQLGetData.**  
  
-   SQL_GD_BOUND. Se essa opção for retornada, **SQLGetData** pode ser chamado para colunas associadas, bem como colunas desassociadas.  
  
 Há duas exceções a essas restrições e capacidade do driver relaxá-los. Primeiro, **SQLGetData** nunca deve ser chamado para um cursor de somente avanço, quando o tamanho do conjunto de linhas for maior que 1. Segundo, se um driver dá suporte a indicadores, ele sempre deve suportar a capacidade de chamar **SQLGetData** para a coluna 0, mesmo se ele não permite que aplicativos chamar **SQLGetData** para outras colunas antes que a última coluna associada. (Quando um aplicativo está trabalhando com um ODBC 2 *. x* driver, **SQLGetData** retornará com êxito um indicador, quando chamado com *Col_or_Param_Num* igual a 0 após uma chamada para **SQLFetch**, pois **SQLFetch** é mapeado por ODBC 3 *. x* Gerenciador de Driver para **SQLExtendedFetch** com um  *FetchOrientation* de SQL_FETCH_NEXT, e **SQLGetData** com um *Col_or_Param_Num* 0 é mapeado por ODBC 3 *. x* para o Gerenciador de Driver **SQLGetStmtOption** com um *fOption* de SQL_GET_BOOKMARK.)  
  
 **SQLGetData** não pode ser usado para recuperar o indicador de uma linha recém-inserida chamando **SQLBulkOperations** com a opção SQL_ADD, porque o cursor não está posicionado na linha. Um aplicativo pode recuperar o indicador para essa linha anexando a coluna 0 antes de chamar **SQLBulkOperations** com SQL_ADD, caso em que **SQLBulkOperations** retorna o indicador no buffer associado. **SQLFetchScroll** , em seguida, pode ser chamado com SQL_FETCH_BOOKMARK para reposicionar o cursor na linha.  
  
 Se o *TargetType* argumento for um tipo de dados de intervalo, a precisão de à esquerda do intervalo de padrão (2) e a precisão de segundos de intervalo padrão (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION do Descartar, respectivamente, são usadas para os dados. Se o *TargetType* argumento é um tipo de dados SQL_C_NUMERIC a precisão padrão (definido pelo driver) e padrão de escala (0), conforme definido nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE a descartar, é usado para os dados. Se qualquer escala ou precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo do descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**. Ele pode definir o campo SQL_DESC_CONCISE_TYPE como SQL_C_NUMERIC e chame **SQLGetData** com um *TargetType* argumento de SQL_ARD_TYPE, o que fará com que os valores de precisão e escala nos campos de descritor para ser usado.  
  
> [!NOTE]  
>  No ODBC 2 *. x*, conjunto de aplicativos *TargetType* SQL_C_DATE, SQL_C_TIME ou SQL_C_TIMESTAMP para indicar que \* *TargetValuePtr* for uma data, hora, ou estrutura de carimbo de hora. Em ODBC 3 *. x*, conjunto de aplicativos *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME ou SQL_C_TYPE_TIMESTAMP. O Gerenciador de Driver torna mapeamentos apropriados se necessário, com base na versão do aplicativo e o driver.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recuperando dados de comprimento variável em partes  
 **SQLGetData** pode ser usado para recuperar dados de uma coluna que contém os dados de comprimento variável em partes — ou seja, quando o identificador do tipo de dados SQL da coluna é SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL _ WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY ou um identificador específico do driver para um tipo de comprimento variável.  
  
 Para recuperar dados de uma coluna em partes, o aplicativo chama **SQLGetData** várias vezes em sucessão para a mesma coluna. Em cada chamada **SQLGetData** retorna a próxima parte dos dados. É responsabilidade do aplicativo para remontar as partes, tomando cuidado para remover o caractere null de terminação de partes intermediários de dados de caracteres. Se houver mais dados para retornar ou não o buffer suficiente foi alocada para o caractere de terminação **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dados truncados). Quando ele retorna a última parte dos dados, **SQLGetData** retorna SQL_SUCCESS. Nem SQL_NO_TOTAL nem zero pode ser retornada na última chamada válida para recuperar dados de uma coluna, porque o aplicativo não teria nenhuma maneira de saber a quantidade de dados no buffer de aplicativo é válido. Se **SQLGetData** é chamado depois disso, ele retornar SQL_NO_DATA. Para obter mais informações, consulte a próxima seção, "Recuperando dados com SQLGetData".  
  
 Indicadores de comprimento variável podem ser retornados em partes por **SQLGetData**. Assim como acontece com outros dados, uma chamada para **SQLGetData** para retornar os indicadores de comprimento variável em partes retornará SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita) e SQL_SUCCESS_WITH_INFO quando há mais dados a serem retornados. Isso é diferente do que o caso quando um indicador de comprimento variável será truncado por uma chamada para **SQLFetch** ou **SQLFetchScroll**, que retorna SQL_ERROR e SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
 **SQLGetData** não pode ser usado para retornar dados de comprimento fixo em partes. Se **SQLGetData** é chamado mais de uma vez em uma linha para uma coluna que contém dados de comprimento fixo, ele retornar SQL_NO_DATA para todas as chamadas feitas depois do primeiro.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperando parâmetros de saída transmitidos  
 Se um driver compatível com os parâmetros de saída em fluxo, um aplicativo pode chamar **SQLGetData** com um pequeno buffer várias vezes para recuperar um valor de parâmetro grande. Para obter mais informações sobre o parâmetro de saída em fluxo, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recuperando dados com SQLGetData  
 Para retornar dados para a coluna especificada, **SQLGetData** executa a seguinte sequência de etapas:  
  
1.  Retorna SQL_NO_DATA se já tiver retornado todos os dados da coluna.  
  
2.  Conjuntos de \* *StrLen_or_IndPtr* como SQL_NULL_DATA se os dados são NULL. Se os dados forem NULL e *StrLen_or_IndPtr* foi um ponteiro nulo, **SQLGetData** retornará SQLSTATE 22002 (variável de indicador necessária, mas não fornecida).  
  
     Se os dados para a coluna não forem NULL, **SQLGetData** continua para a etapa 3.  
  
3.  Se o atributo de instrução de SQL_ATTR_MAX_LENGTH é definido como um valor diferente de zero, se a coluna contiver caracteres ou dados binários e se **SQLGetData** anteriormente não foi chamado para a coluna, os dados são truncados para SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  O atributo da instrução SQL_ATTR_MAX_LENGTH destina-se a reduzir o tráfego de rede. Ele geralmente é implementado pela fonte de dados, que trunca os dados antes de retorná-lo pela rede. Drivers e fontes de dados não são necessários para dar suporte a ele. Portanto, para garantir que os dados são truncados para um tamanho específico, um aplicativo deve alocar um buffer de tamanho e especifique o tamanho no *BufferLength* argumento.  
  
4.  Converte os dados para o tipo especificado em *TargetType*. Os dados são fornecidos a precisão e escala padrão para esse tipo de dados. Se *TargetType* é SQL_ARD_TYPE, os dados de tipo no campo SQL_DESC_CONCISE_TYPE da descartar é usado. Se *TargetType* é SQL_ARD_TYPE, os dados são determinados a precisão e escala em SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, e digite campos SQL_DESC_SCALE de descartar, dependendo dos dados de SQL_DESC_CONCISE Campo de digitar. Se qualquer escala ou precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo do descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
5.  Se os dados foi convertidos em um tipo de dados de comprimento variável, como caractere ou binário, **SQLGetData** verifica se o comprimento dos dados excede *BufferLength*. Se o comprimento dos dados de caracteres (incluindo o caractere null de terminação) exceder *BufferLength*, **SQLGetData** trunca os dados a serem *BufferLength* menos o comprimento de um caractere null de terminação. Em seguida, null-encerra os dados. Se o comprimento dos dados binários excede o comprimento do buffer de dados, **SQLGetData** trunca a *BufferLength* bytes.  
  
     Se o buffer de dados fornecido é muito pequeno para conter o caractere null de terminação, **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01004.  
  
     **SQLGetData** nunca trunca os dados convertidos para dados de comprimento fixo tipos; ele sempre pressupõe que o comprimento de **TargetValuePtr* é o tamanho do tipo de dados.  
  
6.  Coloca os dados convertidos (e possivelmente truncados) em \* *TargetValuePtr*. Observe que **SQLGetData** não podem retornar dados fora de linha.  
  
7.  Coloca o comprimento dos dados de \* *StrLen_or_IndPtr*. Se *StrLen_or_IndPtr* foi um ponteiro nulo, **SQLGetData** não retorna o comprimento.  
  
    -   Para caracteres ou dados binários, esse é o comprimento dos dados após a conversão e antes de truncamento devido a *BufferLength*. Se o driver não pode determinar o comprimento dos dados após a conversão, como às vezes é o caso com dados longos, ele retorna SQL_SUCCESS_WITH_INFO e define o comprimento em SQL_NO_TOTAL. (A última chamada a **SQLGetData** devem sempre retornar o comprimento de dados, e não em zero ou SQL_NO_TOTAL.) Se os dados foram truncados devido à instrução SQL_ATTR_MAX_LENGTH atributo, o valor deste atributo — em vez do comprimento real — é colocado na \* *StrLen_or_IndPtr*. Isso ocorre porque esse atributo foi projetado para truncar os dados no servidor antes da conversão, portanto o driver não tem nenhuma maneira de descobrir que o comprimento real é. Quando **SQLGetData** é chamado várias vezes consecutivas para a mesma coluna, esse é o comprimento dos dados disponíveis no início da chamada atual; isto é, o comprimento diminui com cada chamada subsequente.  
  
    -   Para todos os outros tipos de dados, esse é o comprimento dos dados após a conversão; ou seja, ele é o tamanho do tipo para o qual os dados foi convertidos.  
  
8.  Se os dados são truncados sem perda de significância durante a conversão (por exemplo, o número real 1,234 é truncado quando convertido para o inteiro 1) ou porque *BufferLength* é muito pequeno (por exemplo, a cadeia de caracteres "abcdef" é colocada em um buffer de 4 bytes), **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e o SQLSTATE 01004 (dados truncados). Se os dados são truncados sem perda de significância devido ao atributo de instrução SQL_ATTR_MAX_LENGTH, **SQLGetData** retorna SQL_SUCCESS e não retornará SQLSTATE 01004 (dados truncados).  
  
 O conteúdo do buffer de dados associados (se **SQLGetData** é chamado em uma coluna associada) e o buffer de comprimento/indicador serão definidos se **SQLGetData** não retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
 As chamadas sucessivas para **SQLGetData** recuperará os dados da última coluna solicitada; deslocamentos anteriores se tornam inválidos. Por exemplo, quando a sequência a seguir é executada:  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 a segunda chamada para SQLGetData(icol=n) recupera dados desde o início da coluna n. Deslocamento nos dados devido a chamadas anteriores para **SQLGetData** para a coluna não é válida.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descritores e SQLGetData  
 **SQLGetData** não interagem diretamente com os campos do descritor.  
  
 Se *TargetType* é SQL_ARD_TYPE, os dados de tipo no campo SQL_DESC_CONCISE_TYPE da descartar é usado. Se *TargetType* é SQL_ARD_TYPE ou SQL_C_DEFAULT, os dados são determinados a precisão e escala em SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, e campos SQL_DESC_SCALE de descartar, dependendo dos dados de tipo no campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa um **selecione** instrução para retornar um conjunto de resultados do cliente IDs, nomes e classificados por nome, a ID e o número de telefone de números de telefone. Para cada linha de dados, ele chama **SQLFetch** para posicionar o cursor para a próxima linha. Ele chama **SQLGetData** para recuperar os dados buscados; os buffers para os dados e o número de bytes retornado são especificados na chamada para **SQLGetData**. Por fim, imprime o nome de cada funcionário, ID e número de telefone.  
  
```  
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
|Atribuição de armazenamento para uma coluna em um conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações em massa que não estão relacionados à posição de cursor de bloco|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executar uma instrução SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha de dados ou um bloco de dados em uma direção de somente avanço|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Envio de dados de parâmetro em tempo de execução|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posicionando o cursor, atualizar dados no conjunto de linhas, ou atualizar ou excluir dados no conjunto de linhas|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
