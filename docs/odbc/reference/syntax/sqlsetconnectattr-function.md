---
title: Função SQLSetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aad8baf55dc8960c533e1694309083952dece3d3
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591240"
---
# <a name="sqlsetconnectattr-function"></a>Função SQLSetConnectAttr
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLSetConnectAttr** define os atributos que controlam aspectos de conexões.  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3 *. x* aplicativo está funcionando com um ODBC 2 *. x* driver, consulte [funções de mapeamento de substituição para trás Compatibilidade de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador da conexão*  
 [Entrada] Identificador de Conexão.  
  
 *Atributo*  
 [Entrada] Atributo a ser definido, listados em "Comentários".  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado aos *atributo*. Dependendo do valor de *atributo*, *ValuePtr* será um valor inteiro sem sinal ou apontará para uma cadeia de caracteres terminada em nulo. Observe que o tipo de integral do *atributo* argumento pode não ser de comprimento fixo, consulte a seção comentários para obter detalhes.  
  
 *StringLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer de binário, este argumento deve ser o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* é um inteiro *StringLength* será ignorado.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *StringLength* argumento. *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *StringLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado do SQL_LEN_BINARY_ATTR (*comprimento*) macro na *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, em seguida, *StringLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, então *StringLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *manipular* dos *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetConnectAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
 O driver pode retornar SQL_SUCCESS_WITH_INFO para fornecer informações sobre o resultado de uma opção de configuração.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O driver não oferecia suporte para o valor especificado na *ValuePtr* e substituído, um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08002|Nome da Conexão em uso|O *atributo* argumento era SQL_ATTR_ODBC_CURSORS, e o driver já estava conectado à fonte de dados.|  
|08003|Conexão não aberta|(DM) uma *atributo* foi especificado um valor que necessária uma conexão aberta, mas o *ConnectionHandle* não estava em um estado conectado.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|O *atributo* argumento era SQL_ATTR_CURRENT_CATALOG e um conjunto de resultados estava pendente.|  
|25000|Operação ilegal enquanto estiver em uma transação local|Uma conexão foi em uma transação local durante a tentativa de se inscrever em uma conexão de transações distribuídas (DTC), definindo o atributo de conexão SQL_ATTR_ENLIST_IN_DTC.<br /><br /> Uma conexão já está inscrito em um DTC.<br /><br /> Uma conexão foi inscrito em uma conexão de transação distribuída e uma transação local foi iniciada, definindo SQL_ATTR_AUTOCOMMIT como SQL_AUTOCOMMIT_OFF.|  
|3D000|Nome de catálogo inválido|O *atributo* argumento era SQL_CURRENT_CATALOG, e o nome de catálogo especificado era inválido.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. O **SQLSetConnectAttr** função foi chamada e antes ele concluiu a execução, o [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado no *ConnectionHandle*e, em seguida, o **SQLSetConnectAttr** função foi chamada novamente sobre o *ConnectionHandle*.<br /><br /> Ou, o **SQLSetConnectAttr** função foi chamada e antes ele concluiu a execução, **SQLCancelHandle** foi chamado no *ConnectionHandle* de um thread diferente no um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O *atributo* argumento identificado um atributo de conexão que é necessário um valor de cadeia de caracteres, e o *ValuePtr* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um *StatementHandle* associado com o *ConnectionHandle* e ainda estava em execução quando **SQLSetConnectAttr**foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas com o *ConnectionHandle* e retornado SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para um *StatementHandle*  associado com o *ConnectionHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) **SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornado SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|HY011|Atributo não pode ser definido agora|O *atributo* argumento era SQL_ATTR_TXN_ISOLATION, e uma transação foi aberta.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY024|Valor de atributo inválido|Dado especificado *atributo* valor, um valor inválido foi especificado na *ValuePtr*. (O Gerenciador de Driver retorna esse SQLSTATE apenas para conexão e atributos de instrução que aceitam um conjunto discreto de valores, como SQL_ATTR_ACCESS_MODE ou SQL_ATTR_ASYNC_ENABLE. Para todas as outras conexão e atributos de instrução, o driver deve verificar o valor especificado na *ValuePtr*.)<br /><br /> O *atributo* argumento era SQL_ATTR_TRACEFILE ou SQL_ATTR_TRANSLATE_LIB, e *ValuePtr* foi uma cadeia de caracteres vazia.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|*(DM) \*ValuePtr* é uma cadeia de caracteres e o *StringLength* argumento era menor que 0 mas não estavam SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.<br /><br /> (DM) o valor especificado para o argumento *atributo* era um atributo somente leitura.|  
|HY114|Driver não oferece suporte à execução de função de nível de conexão assíncrona|Tentativa de um aplicativo (DM) habilitar a execução de função assíncrona com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE um driver que não dá suporte a operações de conexão assíncrona.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|Biblioteca de cursores e o pool de reconhecimento de Driver não podem ser habilitada ao mesmo tempo|Para obter mais informações, consulte [Pooling de Conexão de reconhecimento de Driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* foi uma conexão ODBC válida ou o atributo de instrução para a versão do ODBC com suporte pelo driver, mas não tinha suporte pelo driver.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *ConnectionHandle* não suporta a função.|  
|IM009|Não é possível carregar a DLL de conversão|O driver não pôde carregar a DLL que foi especificado para a conexão de tradução. Esse erro pode ser retornado apenas quando *atributo* é SQL_ATTR_TRANSLATE_LIB.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
|S1118|Driver não oferece suporte a notificação assíncrona|SQL_ATTR_ASYNC_DBC_EVENT foi definido (depois que a conexão foi feita), mas não há suporte para notificação assíncrona pelo driver.|  
  
 Quando *atributo* é um atributo de instrução **SQLSetConnectAttr** pode retornar qualquer SQLSTATEs retornados por **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre os atributos de conexão, consulte [atributos de Conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Os atributos definidos no momento e a versão do ODBC na qual eles foram introduzidos são mostrados na tabela mais adiante nesta seção; é esperado que serão definidos atributos mais para tirar proveito de diferentes fontes de dados. Um intervalo de atributos é reservado pelo ODBC; os desenvolvedores de driver deverá reservar os valores para seu próprio uso específico do driver do Open Group.  
  
> [!NOTE]
>  A capacidade de definir atributos de instrução no nível de conexão chamando **SQLSetConnectAttr** foi preterido no ODBC 3 *. x*. 3 de ODBC *. x* aplicativos nunca devem definir atributos de instrução no nível de conexão. 3 de ODBC *. x* atributos de instrução não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de instrução e pode ser definido no nível de conexão ou o nível de instrução.  
> 
>  3 de ODBC *. x* drivers precisam dar suporte apenas essa funcionalidade se eles devem funcionar com o ODBC 2 *. x* aplicativos que definam o ODBC 2 *. x* opções da instrução no nível de conexão. Para obter mais informações, consulte [mapeamento SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no Apêndice g: Diretrizes de driver para compatibilidade com versões anteriores.  
  
 Um aplicativo pode chamar **SQLSetConnectAttr** a qualquer momento entre o momento em que a conexão é alocado e liberado. Todos os atributos de conexão e instrução definidos com êxito pelo aplicativo para a conexão persistem até **SQLFreeHandle** é chamado de conexão. Por exemplo, se um aplicativo chamar **SQLSetConnectAttr** antes de se conectar a uma fonte de dados, o atributo persiste mesmo se **SQLSetConnectAttr** falhar no driver quando o aplicativo se conecta à fonte de dados; Se um aplicativo define um atributo específico do driver, o atributo persiste mesmo se o aplicativo se conecta a um driver diferente sobre a conexão.  
  
 Alguns atributos de conexão podem ser definidos apenas antes que uma conexão foi feita; outras pessoas podem ser definidas somente depois que uma conexão foi feita. A tabela a seguir indica os atributos de conexão devem ser definidos antes ou depois que uma conexão é feita. *Qualquer um dos* indica que o atributo pode ser definido antes ou depois da conexão.  
  
|attribute|Defina antes ou depois da conexão?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|Qualquer|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|Qualquer|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|Qualquer|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|Qualquer|  
|SQL_ATTR_AUTOCOMMIT|[5]|  
|SQL_ATTR_CONNECTION_DEAD|After (após)|  
|SQL_ATTR_CONNECTION_TIMEOUT|Qualquer|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After (após)|  
|SQL_ATTR_ENLIST_IN_DTC|After (após)|  
|SQL_ATTR_LOGIN_TIMEOUT|Antes de|  
|SQL_ATTR_METADATA_ID|Qualquer|  
|SQL_ATTR_ODBC_CURSORS|Antes de|  
|SQL_ATTR_PACKET_SIZE|Antes de|  
|SQL_ATTR_QUIET_MODE|Qualquer|  
|SQL_ATTR_TRACE|Qualquer|  
|SQL_ATTR_TRACEFILE|Qualquer|  
|SQL_ATTR_TRANSLATE_LIB|After (após)|  
|SQL_ATTR_TRANSLATE_OPTION|After (após)|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE e SQL_ATTR_CURRENT_CATALOG podem ser definidos antes ou depois de conectar-se de que, dependendo do driver. No entanto, aplicativos interoperáveis definem-las antes de se conectar porque alguns drivers não dão suporte para a alteração delas após a conexão.  
  
 [2] SQL_ATTR_ASYNC_ENABLE deve ser definida antes que haja uma instrução ativa.  
  
 [3] SQL_ATTR_TXN_ISOLATION pode ser definido somente se não houver nenhuma transação aberta sobre a conexão. Alguns atributos de conexão oferecem suporte à substituição de um valor semelhante se a fonte de dados não dá suporte para o valor especificado na \* *ValuePtr*. Nesses casos, o driver retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor de opção alterado). Por exemplo, se *atributo* é SQL_ATTR_PACKET_SIZE e \* *ValuePtr* excede o tamanho máximo do pacote, o driver substitui o tamanho máximo. Para determinar o valor substituído, um aplicativo chama **SQLGetConnectAttr**.  
  
 [4] se SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE for definido antes de uma conexão está aberta, o Gerenciador de Driver definirá os atributos do driver quando o driver é carregado durante uma chamada para **SQLBrowseConnect**, **SQLConnect**, ou **SQLDriverConnect**. Antes de uma chamada para **SQLBrowseConnect**, **SQLConnect**, ou **SQLDriverConnect**, o Gerenciador de Driver não sabe qual driver para se conectar ao e não sabe se a driver dá suporte a operações de conexão assíncrona. Portanto, o Gerenciador de Driver sempre retorna SQL_SUCCESS. Mas, caso o driver não oferece suporte a operações assíncronas de conexão, a chamada para **SQLBrowseConnect**, **SQLConnect**, ou **SQLDriverConnect** falhará.  
  
 [5] quando SQL_ATTR_AUTOCOMMIT é definido como FALSE, os aplicativos devem chamar SQLEndTran(SQL_ROLLBACK) se qualquer API retornará SQL_ERROR para garantir a consistência transacional.  
  
 O formato de informações definidas \* *ValuePtr* buffer depende do especificado *atributo*. **SQLSetConnectAttr** aceitará as informações de atributo em um dos dois formatos diferentes: uma cadeia de caracteres terminada em nulo ou um valor inteiro. O formato de cada um é indicado na descrição do atributo. Apontada por cadeias de caracteres a *ValuePtr* argumento de **SQLSetConnectAttr** ter um comprimento de *StringLength* bytes.  
  
 O *StringLength* argumento será ignorado se o comprimento é definido pelo atributo, como é o caso para todos os atributos introduzidas no ODBC 2 *. x* ou anterior.  
  
|*Atributo*|*ValuePtr* conteúdo|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|Um valor SQLUINTEGER. SQL_MODE_READ_ONLY é usado pelo driver ou fonte de dados como um indicador de que a conexão não é necessário para dar suporte a instruções SQL que fazem com que as atualizações ocorram. Esse modo pode ser usado para otimizar estratégias de bloqueio, gerenciamento de transações ou outras áreas conforme apropriado para a driver ou fonte de dados. O driver não é necessário para evitar tais instruções sejam enviados à fonte de dados. O comportamento do driver e fonte de dados quando for solicitado para processar instruções SQL que não são somente leitura durante uma conexão somente leitura é definido pela implementação. SQL_MODE_READ_WRITE é o padrão.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|Um valor SQLPOINTER que é um identificador de eventos.<br /><br /> Notificação da conclusão de funções assíncronas está habilitada por meio da chamada **SQLSetConnectAttr** com o atributo SQL_ATTR_ASYNC_STMT_EVENT e especificando o identificador de eventos. **Observação:**  Não há suporte para o método de notificação com a biblioteca de cursores. Um aplicativo receberá a mensagem de erro se tentar habilitar a biblioteca de cursores por meio do SQLSetConnectAttr, quando o método de notificação está habilitado.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|Um valor SQLUINTEGER que habilita ou desabilita a execução assíncrona de funções selecionadas no identificador de conexão. Para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = operação assíncrona para habilitar para funções relacionadas à conexão especificadas.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (padrão) desabilitar a operação assíncrona para funções relacionadas à conexão especificadas.<br /><br /> Definindo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE sempre é síncrono (ou seja, ele nunca retornará SQL_STILL_EXECUTING).<br /><br /> Execução assíncrona de operações de instrução são habilitados com SQL_ATTR_ASYNC_ENABLE.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Um valor SQLPOINTER que aponta para a estrutura de contexto.<br /><br /> Somente o Gerenciador de Driver pode chamar um driver **SQLSetStmtAttr** função com esse atributo.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Um valor SQLPOINTER que aponta para a estrutura de contexto.<br /><br /> Somente o Gerenciador de Driver pode chamar um driver **SQLSetStmtAttr** função com esse atributo.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|Um valor SQLULEN que especifica se uma função chamada com uma instrução em que a conexão especificada é executada de forma assíncrona:<br /><br /> SQL_ASYNC_ENABLE_OFF = desabilitar o suporte de nível de execução assíncrona de conexão para operações de instrução (o padrão).<br /><br /> SQL_ASYNC_ENABLE_ON = Habilitar suporte de nível de execução assíncrona de conexão para operações de instrução.<br /><br /> Esse atributo pode ser definido se **SQLGetInfo** com as informações de SQL_ASYNC_MODE tipo retorna SQL_AM_CONNECTION ou SQL_AM_STATEMENT.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|Um valor de sqluinteger que contém somente leitura que especifica se a população automática do IPD após uma chamada para **SQLPrepare** há suporte para:<br /><br /> SQL_TRUE = população automática do IPD após uma chamada para **SQLPrepare** tem suporte pelo driver.<br /><br /> SQL_FALSE = população automática do IPD após uma chamada para **SQLPrepare** não tem suporte pelo driver. Servidores que não dão suporte a instruções preparadas não poderá preencher o IPD automaticamente.<br /><br /> Se SQL_TRUE for retornado para o atributo de conexão SQL_ATTR_AUTO_IPD, o atributo de instrução SQL_ATTR_ENABLE_AUTO_IPD pode ser definido para ativar ou desativar a população automática do IPD. Se SQL_ATTR_AUTO_IPD for SQL_FALSE, SQL_ATTR_ENABLE_AUTO_IPD não pode ser definido como SQL_TRUE. O valor padrão de SQL_ATTR_ENABLE_AUTO_IPD é igual ao valor de SQL_ATTR_AUTO_IPD.<br /><br /> Esse atributo de conexão pode ser retornado por **SQLGetConnectAttr** mas não pode ser definida por **SQLSetConnectAttr**.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|Um valor SQLUINTEGER que especifica se deve usar o modo de confirmação automática ou manual de confirmação:<br /><br /> SQL_AUTOCOMMIT_OFF = o driver usa o modo de confirmação manual e o aplicativo deve confirmar ou reverter transações com explicitamente **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = o driver usa o modo confirmação automática. Cada instrução é confirmada imediatamente após ele é executado. Esse é o padrão. Qualquer transação aberta sobre a conexão serão confirmadas quando SQL_ATTR_AUTOCOMMIT é definido como SQL_AUTOCOMMIT_ON alterar do modo de confirmação manual para o modo de confirmação automática.<br /><br /> Para obter mais informações, consulte [modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md). **Importante:**  Algumas fontes de dados excluir os planos de acesso e fechar os cursores para todas as instruções em uma conexão sempre que uma instrução é confirmada. modo de confirmação automática pode fazer com que isso aconteça após cada instrução nonquery é executada ou quando o cursor será fechado para uma consulta. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [efeito de transações em cursores e instruções preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md). <br /><br /> Quando um lote é executado no modo de confirmação automática, duas coisas são possíveis. O lote inteiro pode ser tratado como uma unidade de autocommitable ou cada instrução em um lote é tratada como uma unidade de autocommitable. Certas fontes de dados podem dar suporte a ambos os esses comportamentos e podem fornecer uma maneira de escolher um ou outro. Ele é definido pelo driver se um lote é tratado como uma unidade de autocommitable ou se cada instrução individual dentro do lote é autocommitable.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|Um valor de sqluinteger que contém somente leitura que indica o estado da conexão. Se SQL_CD_TRUE, a conexão foi perdida. Se SQL_CD_FALSE, a conexão ainda está ativa.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|Um valor SQLUINTEGER correspondente ao número de segundos a aguardar para qualquer solicitação de conexão para ser concluída antes de retornar ao aplicativo. O driver deve retornar SQLSTATE HYT00 (tempo limite expirado) a qualquer momento que ela é possível atingir o tempo limite em uma situação não associado com a execução da consulta ou de logon.<br /><br /> Se *ValuePtr* é igual a 0 (o padrão), não há nenhum tempo limite.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|Uma cadeia de caracteres que contém o nome do catálogo a ser usado pela fonte de dados. Por exemplo, no SQL Server, o catálogo é um banco de dados, portanto, o driver envia um **uso** _banco de dados_ instrução à fonte de dados, onde *banco de dados* é o banco de dados especificado em \* *ValuePtr*. Para um driver de camada única, o catálogo pode ser um diretório, portanto, o driver altera seu diretório atual para o diretório especificado no **ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|Um valor SQLPOINTER usado para definir novamente o token de informações de conexão para o DBC lidar com quando [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)do (\**pRating*) parâmetro não é igual a 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN é somente de conjunto. Não é possível usar **SQLGetConnectAttr** ou **SQLGetConnectOption** para recuperar esse valor. O Gerenciador de Driver **SQLSetConnectAttr** não aceitará SQL_ATTR_DBC_INFO_TOKEN, uma vez que um aplicativo não deve definir esse atributo.<br /><br /> Se um driver retornará SQL_ERROR depois de definir SQL_ATTR_DBC_INFO_TOKEN, a conexão apenas é obtido do pool será liberada. O Gerenciador de Driver, em seguida, tentará obter outra conexão do pool. Ver [desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) para obter mais informações.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Um valor SQLPOINTER que especifica se deve usar o driver ODBC em transações distribuídas coordenadas por serviços de componentes da Microsoft.<br /><br /> Passe um DTC OLE objeto de transação que especifica a transação para exportar para SQL Server ou SQL_DTC_DONE para encerrar a associação de DTC da conexão.<br /><br /> O cliente chama o método de Microsoft Distributed Transaction Coordinator (MS DTC) OLE itransactiondispenser:: BeginTransaction para iniciar uma transação do MS DTC e criar um objeto de transação do MS DTC que representa a transação. O aplicativo, em seguida, chama SQLSetConnectAttr com a opção SQL_ATTR_ENLIST_IN_DTC para associar o objeto de transação com a conexão ODBC. Todas as atividades de banco de dados relacionadas serão executadas sob a proteção da transação do MS DTC. O aplicativo chama SQLSetConnectAttr com SQL_DTC_DONE para encerrar a associação de DTC da conexão. Para obter mais informações, consulte a documentação do MS DTC.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|Um valor SQLUINTEGER correspondente ao número de segundos a aguardar uma solicitação de logon para concluir antes de retornar ao aplicativo. O padrão é dependente do driver. Se *ValuePtr* é 0, o tempo limite será desabilitado e uma tentativa de conexão aguardará indefinidamente.<br /><br /> Se o tempo limite especificado excede o tempo de limite máximo de logon na fonte de dados, o driver substitui esse valor e retorna um SQLSTATE 01S02 (valor de opção alterado).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Um valor SQLUINTEGER que determina como os argumentos de cadeia de caracteres das funções de catálogo são tratados.<br /><br /> Se SQL_TRUE, o argumento de cadeia de caracteres das funções de catálogo são tratadas como identificadores. Caso não é significativo. Para cadeias de caracteres proibidas, o driver remove os espaços à direita e a cadeia de caracteres é armazenada em maiusculas. Para cadeias de caracteres delimitadas, o driver remove espaços à esquerda ou à direita e leva, literalmente, tudo o que está entre os delimitadores. Se um desses argumentos é definido como um ponteiro nulo, a função retornará SQL_ERROR e SQLSTATE HY009 (uso inválido de ponteiro nulo).<br /><br /> Se SQL_FALSE, os argumentos de cadeia de caracteres das funções de catálogo não são tratadas como identificadores. O caso é significativo. Eles podem conter um padrão de pesquisa de cadeia de caracteres ou não, dependendo do argumento.<br /><br /> O valor padrão é SQL_FALSE.<br /><br /> O *TableType* argumento de **SQLTables**, que usa uma lista de valores, não é afetada por este atributo.<br /><br /> SQL_ATTR_METADATA_ID também podem ser definidas no nível de instrução. (É o atributo de conexão única que é também um atributo de instrução).<br /><br /> Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Um valor SQLULEN Especifica como o Gerenciador de Driver usa a biblioteca de cursores ODBC:<br /><br /> SQL_CUR_USE_IF_NEEDED = o Gerenciador de Driver usa a biblioteca de cursores ODBC somente se ele for necessário. Se o driver dá suporte à opção SQL_FETCH_PRIOR na **SQLFetchScroll**, o Gerenciador de Driver usa os recursos de rolagem do driver. Caso contrário, ele usa a biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_ODBC = o Gerenciador de Driver usa a biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_DRIVER = o Gerenciador de Driver usa os recursos de rolagem do driver. Essa é a configuração padrão.<br /><br /> Para obter mais informações sobre a biblioteca de cursores ODBC, consulte [apêndice f: Biblioteca de cursores ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md). **Aviso:**  A biblioteca de cursores será removida em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|Um valor SQLUINTEGER especificando o tamanho do pacote de rede em bytes. **Observação:**  Muitas fontes de dados não suportam essa opção ou apenas retornada mas não podem definir o tamanho do pacote de rede. <br /><br /> Se o tamanho especificado excede o tamanho máximo do pacote ou é menor do que o tamanho mínimo do pacote, o driver substitui esse valor e retorna um SQLSTATE 01S02 (valor de opção alterado).<br /><br /> Se o aplicativo define o tamanho do pacote depois que uma conexão já foi feita, o driver retornará SQLSTATE HY011 (atributo não pode ser definido agora).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|Um identificador de janela (HWND).<br /><br /> Se o identificador de janela é um ponteiro nulo, o driver não exibe nenhuma caixa de diálogo.<br /><br /> Se o identificador de janela não for um ponteiro nulo, ele deve ser o identificador de janela pai do aplicativo. Esse é o padrão. O driver usa esse identificador para exibir caixas de diálogo. **Observação:**  O atributo de conexão SQL_ATTR_QUIET_MODE não se aplica às caixas de diálogo exibidas pelo **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1.0)|Um valor de sqluinteger que contém o Gerenciador de Driver de dizer se deseja executar o rastreamento:<br /><br /> SQL_OPT_TRACE_OFF = rastreamento desativado (padrão)<br /><br /> SQL_OPT_TRACE_ON = rastreamento ativado<br /><br /> Quando o rastreamento está ativado, o Gerenciador de Driver grava cada chamada de função ODBC para o arquivo de rastreamento. **Observação:**  Quando o rastreamento está ativado, o Gerenciador de Driver pode retornar SQLSTATE IM013 (erro de arquivo de rastreamento) de qualquer função. <br /><br /> Um aplicativo especifica um arquivo de rastreamento com a opção SQL_ATTR_TRACEFILE. Se o arquivo já existir, o Gerenciador de Driver acrescenta ao arquivo. Caso contrário, ele cria o arquivo. Se o rastreamento estiver ligado e nenhum arquivo de rastreamento foi especificado, o Gerenciador de Driver grava no arquivo SQL. Faça logon no diretório raiz.<br /><br /> Um aplicativo pode definir a variável **ODBCSharedTraceFlag** para ativar o rastreamento dinamicamente. Em seguida, o rastreamento está habilitado para todos os aplicativos ODBC em execução no momento. Se um aplicativo desativa o rastreamento, ele é desativado para o aplicativo.<br /><br /> Se o **rastreamento** palavra-chave nas informações do sistema é definido como 1, quando um aplicativo chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV, o rastreamento está habilitado para todos manipula. Ela é habilitada somente para o aplicativo que chamou **SQLAllocHandle**.<br /><br /> Chamando **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_TRACE não requer que o *ConnectionHandle* argumento seja válido e não retornará SQL_ERROR se *ConnectionHandle* é NULL. Este atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Uma cadeia de caracteres com terminação nula que contém o nome do arquivo de rastreamento.<br /><br /> O valor padrão do atributo SQL_ATTR_TRACEFILE é especificado com o **TraceFile** palavra-chave nas informações do sistema. Para obter mais informações, consulte [subchave ODBC](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Chamando **SQLSetConnectAttr** com um *atributo* de sql_attr TRACEFILE não exigem o *ConnectionHandle* argumento seja válido e não retornará SQL_ERROR se *ConnectionHandle* é inválido. Este atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Uma cadeia de caracteres de terminação nula que contém o nome de uma biblioteca que contém as funções **SQLDriverToDataSource** e **SQLDataSourceToDriver** que o driver acessa para executar tarefas, como tradução do conjunto de caracteres. Essa opção pode ser especificado somente se o driver conectou-se à fonte de dados. A configuração deste atributo persistirá em conexões. Para obter mais informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md) e [referência de função de DLL de conversão](../../../odbc/reference/syntax/translation-dll-api-reference.md).|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|Um valor de sinalizador de 32 bits que é passado para a DLL de conversão. Esse atributo pode ser especificado somente se o driver conectou-se à fonte de dados. Para obter informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|Um bitmask de 32 bits que define o nível de isolamento de transação para a conexão atual. Um aplicativo deve chamar **SQLEndTran** para confirmar ou reverter todas as transações abertas em uma conexão, antes de chamar **SQLSetConnectAttr** com essa opção.<br /><br /> Os valores válidos para *ValuePtr* pode ser determinado chamando **SQLGetInfo** com *tipo de informação* igual a SQL_TXN_ISOLATION_OPTIONS.<br /><br /> Para obter uma descrição dos níveis de isolamento da transação, consulte a descrição do tipo de informações SQL_DEFAULT_TXN_ISOLATION na [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [níveis de isolamento da transação](../../../odbc/reference/develop-app/transaction-isolation-levels.md).|  
  
 [1] dessas funções podem ser chamadas de forma assíncrona somente se o descritor é um descritor de implementação, não um descritor de aplicativo.  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
