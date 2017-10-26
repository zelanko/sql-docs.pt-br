---
title: "Função SQLSetConnectAttr | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 83
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4006d05403781ada24cf43903cd14a971366e12a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattr-function"></a>Função SQLSetConnectAttr
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLSetConnectAttr** define os atributos que controlam aspectos de conexões.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3*. x* aplicativo estiver trabalhando com um ODBC 2*. x* driver, consulte [mapeamento de funções de substituição para recuar Compatibilidade de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 [Entrada] Atributo a ser definido, listadas em "Comentários".  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado aos *atributo*. Dependendo do valor de *atributo*, *ValuePtr* será um valor inteiro não assinado ou aponta para uma cadeia de caracteres terminada em nulo. Observe que a base integral de tipo do *atributo* argumento pode não ser de comprimento fixo, consulte a seção comentários para obter detalhes.  
  
 *StringLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer binário, este argumento deve ser o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* é um inteiro, *StringLength* será ignorado.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *StringLength* argumento. *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *StringLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado da SQL_LEN_BINARY_ATTR (*comprimento*) macro em *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, em seguida, *StringLength* devem ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contém um valor de comprimento fixo, em seguida, *StringLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLSetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *tratar* de *identificador da conexão*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetConnectAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
 O driver pode retornar SQL_SUCCESS_WITH_INFO para fornecer informações sobre o resultado de uma opção de configuração.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O driver não oferecia suporte ao valor especificado em *ValuePtr* e substituído, um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08002|Nome da Conexão em uso|O *atributo* argumento era SQL_ATTR_ODBC_CURSORS, e o driver já foi conectado à fonte de dados.|  
|08003|Conexão não aberta|(DM) um *atributo* foi especificado um valor que necessária uma conexão aberta, mas o *identificador da conexão* não estava em um estado conectado.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|O *atributo* argumento SQL_ATTR_CURRENT_CATALOG, e um conjunto de resultados era pendente.|  
|25000|Operação ilegal enquanto estiver em uma transação local|Uma conexão foi em uma transação local ao tentar se inscrever em uma conexão de transações distribuídas (DTC), definindo o atributo de conexão SQL_ATTR_ENLIST_IN_DTC.<br /><br /> Uma conexão já está inscrita em um DTC.<br /><br /> Uma conexão tem foi inscrita em uma conexão de transação distribuída e uma transação local foi iniciada, definindo SQL_ATTR_AUTOCOMMIT como SQL_AUTOCOMMIT_OFF.|  
|3D000|Nome de catálogo inválido|O *atributo* argumento SQL_CURRENT_CATALOG, e o nome de catálogo especificado era inválido.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *identificador da conexão*. O **SQLSetConnectAttr** função foi chamada e antes ele concluiu a execução, o [SQLCancelHandle função](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado no *identificador da conexão*e, em seguida, o **SQLSetConnectAttr** função foi chamada novamente no *identificador da conexão*.<br /><br /> Ou, o **SQLSetConnectAttr** função foi chamada e antes ele concluiu a execução, **SQLCancelHandle** foi chamado no *identificador da conexão* de um thread diferente no um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O *atributo* argumento identificado um atributo de conexão que é necessário um valor de cadeia de caracteres, e o *ValuePtr* argumento era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um *StatementHandle* associados a *identificador da conexão* e ainda estava em execução quando **SQLSetConnectAttr**foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *identificador da conexão* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas a *identificadordaconexão* e retornado SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para um *StatementHandle * associados a *identificador da conexão* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) **SQLBrowseConnect** foi chamado para o *identificador da conexão* e retorna SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornado SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|HY011|Atributo não pode ser definido agora|O *atributo* argumento era SQL_ATTR_TXN_ISOLATION, e uma transação foi aberta.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY024|Valor de atributo inválido|Dado especificado *atributo* valor, um valor inválido foi especificado na *ValuePtr*. (O Gerenciador de Driver retorna esse SQLSTATE apenas para a conexão e os atributos de instrução que aceitam um conjunto separado de valores, como SQL_ATTR_ACCESS_MODE ou SQL_ATTR_ASYNC_ENABLE. Para todos os outros conexão e atributos de instrução, o driver deve verificar o valor especificado em *ValuePtr*.)<br /><br /> O *atributo* argumento era SQL_ATTR_TRACEFILE ou SQL_ATTR_TRANSLATE_LIB, e *ValuePtr* era uma cadeia de caracteres vazia.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|*(DM) \*ValuePtr* é uma cadeia de caracteres e o *StringLength* argumento era menor que 0 mas não estavam SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.<br /><br /> (DM) o valor especificado para o argumento *atributo* era um atributo somente leitura.|  
|HY114|Driver não oferece suporte à execução de função assíncrona de nível de conexão|Tentativa de um aplicativo (DM) habilitar a execução de função assíncrona com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para um driver que não oferece suporte a operações de conexão assíncrona.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|Biblioteca de cursores e pool com reconhecimento de Driver não podem ser habilitada ao mesmo tempo|Para obter mais informações, consulte [Pooling de Conexão com reconhecimento de Driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* foi uma conexão ODBC válida ou atributo de instrução para a versão do ODBC com suporte pelo driver, mas não era compatível com o driver.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *identificador da conexão* não oferece suporte para a função.|  
|IM009|Não é possível carregar a DLL de conversão|O driver não pôde carregar a DLL que foi especificado para a conexão de conversão. Esse erro pode ser retornado apenas quando *atributo* é SQL_ATTR_TRANSLATE_LIB.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
|S1118|Driver não dá suporte a notificação assíncrona|SQL_ATTR_ASYNC_DBC_EVENT foi definido (depois que a conexão foi feita), mas não há suporte para a notificação assíncrona pelo driver.|  
  
 Quando *atributo* é um atributo de instrução, **SQLSetConnectAttr** pode retornar qualquer SQLSTATEs retornados por **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre os atributos de conexão, consulte [atributos de Conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Os atributos definidos atualmente e a versão do ODBC no qual eles foram apresentados são mostrados na tabela mais adiante nesta seção; espera-se que mais atributos serão definidos para tirar proveito de diferentes fontes de dados. Um intervalo de atributos é reservado pelo ODBC; os desenvolvedores de driver devem reservar valores para seu próprio uso específico do driver do Open Group.  
  
> [!NOTE]  
>  A capacidade de definir atributos de instrução no nível de conexão chamando **SQLSetConnectAttr** foi preterido no ODBC 3*. x*. ODBC 3*. x* aplicativos nunca devem definir atributos de instrução no nível de conexão. ODBC 3*. x* atributos de instrução não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de instrução e pode ser definir o nível de conexão ou o nível de instrução.  
>   
>  ODBC 3*. x* drivers necessitam suporte para essa funcionalidade somente se eles devem funcionar com ODBC 2*. x* aplicativos que definam o ODBC 2*. x* opções da instrução no nível de conexão. Para obter mais informações, consulte [SQLSetConnectOption mapeamento](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
 Um aplicativo pode chamar **SQLSetConnectAttr** a qualquer momento entre o momento em que a conexão é alocada e liberado. Todos os atributos de conexão e instrução definidos com êxito pelo aplicativo para a conexão persistem até **SQLFreeHandle** é chamado de conexão. Por exemplo, se um aplicativo chamar **SQLSetConnectAttr** antes de se conectar a uma fonte de dados, o atributo persiste mesmo se **SQLSetConnectAttr** falha no driver quando o aplicativo se conecta à fonte de dados; Se um aplicativo define um atributo específico do driver, o atributo persiste mesmo se o aplicativo se conecta a um driver diferente em que a conexão.  
  
 Alguns atributos de conexão podem ser definidos apenas antes de uma conexão foi feita; outras podem ser definidas somente depois que uma conexão é estabelecida. A tabela a seguir indica os atributos de conexão devem ser definidos antes ou depois que uma conexão é estabelecida. *Qualquer* indica que o atributo pode ser definido antes ou depois da conexão.  
  
|Atributo|Defina antes ou após a conexão?|  
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
  
 [1] SQL_ATTR_ACCESS_MODE e SQL_ATTR_CURRENT_CATALOG podem ser definidas antes ou depois de conectar-se de que, dependendo do driver. No entanto, os aplicativos interoperáveis definem-las antes de se conectar porque alguns drivers não dão suporte ao alterar esses depois de se conectar.  
  
 [2] SQL_ATTR_ASYNC_ENABLE deve ser definida antes que haja uma instrução ativa.  
  
 [3] SQL_ATTR_TXN_ISOLATION pode ser definido somente se não houver nenhuma transação aberta sobre a conexão. Alguns atributos de conexão oferecem suporte à substituição de um valor semelhante se a fonte de dados não dá suporte para o valor especificado em \* *ValuePtr*. Nesses casos, o driver retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado). Por exemplo, se *atributo* é SQL_ATTR_PACKET_SIZE e \* *ValuePtr* excede o tamanho máximo do pacote, o driver substitui o tamanho máximo. Para determinar o valor substituído, um aplicativo chama **SQLGetConnectAttr**.  
  
 [4] se SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE é definida antes que uma conexão está aberta, o Gerenciador de Driver será definida atributo do driver quando o driver é carregado durante uma chamada para **SQLBrowseConnect**, **SQLConnect**, ou **SQLDriverConnect**. Antes de uma chamada para **SQLBrowseConnect**, **SQLConnect**, ou **SQLDriverConnect**, o Gerenciador de Driver não sabe qual driver para se conectar ao e não sabe se a driver dá suporte a operações de conexão assíncrona. Portanto, o Gerenciador de Driver sempre retorna SQL_SUCCESS. Mas, no caso do driver não oferece suporte a operações de conexão assíncrona, a chamada para **SQLBrowseConnect**, **SQLConnect**, ou **SQLDriverConnect** falhará.  
  
 [5] ao SQL_ATTR_AUTOCOMMIT é definido como FALSE, os aplicativos devem chamar SQLEndTran(SQL_ROLLBACK) se qualquer API retornará SQL_ERROR para garantir a consistência transacional.  
  
 O formato do conjunto informações de \* *ValuePtr* buffer depende de especificado *atributo*. **SQLSetConnectAttr** aceitará as informações de atributo em um dos dois formatos diferentes: uma cadeia de caracteres terminada em nulo ou um valor inteiro. O formato de cada um é indicado na descrição do atributo. Apontada por cadeias de caracteres de *ValuePtr* argumento de **SQLSetConnectAttr** ter um comprimento de *StringLength* bytes.  
  
 O *StringLength* argumento será ignorado se o comprimento é definido pelo atributo, como é o caso para todos os atributos introduzidas no ODBC 2*. x* ou anterior.  
  
|*Atributo*|*ValuePtr* conteúdo|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|Um valor SQLUINTEGER. SQL_MODE_READ_ONLY é usado pelo driver ou fonte de dados como um indicador de que a conexão não é necessário para dar suporte a instruções SQL que fazer com que as atualizações ocorram. Esse modo pode ser usado para otimizar as estratégias de proteção, gerenciamento de transações ou outras áreas conforme for apropriado para a driver ou fonte de dados. O driver não é necessário para evitar tais instruções que estão sendo enviadas à fonte de dados. O comportamento do driver e fonte de dados quando for solicitado para processar instruções SQL que não são somente leitura durante uma conexão somente leitura é definido pela implementação. SQL_MODE_READ_WRITE é o padrão.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|Um valor SQLPOINTER é um identificador de evento.<br /><br /> Notificação de conclusão de funções assíncronas é ativada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_ASYNC_STMT_EVENT e especificando o identificador de eventos. **Observação:** não há suporte para o método de notificação com a biblioteca de cursores. Um aplicativo recebe a mensagem de erro ao tentar habilitar a biblioteca de cursores por meio do SQLSetConnectAttr, quando o método de notificação está habilitado.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|Um valor SQLUINTEGER que habilita ou desabilita a execução assíncrona de funções selecionadas no identificador da conexão. Para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = Enable a operação assíncrona para funções relacionadas à conexão especificadas.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = Disable (padrão) a operação assíncrona para funções relacionadas à conexão especificadas.<br /><br /> Configuração SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE sempre é síncrono (ou seja, ele nunca retornará SQL_STILL_EXECUTING).<br /><br /> Execução assíncrona de operações de instrução são habilitados com SQL_ATTR_ASYNC_ENABLE.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Um valor SQLPOINTER que aponta para a estrutura de contexto.<br /><br /> Somente o Gerenciador de Driver pode chamar um driver **SQLSetStmtAttr** função com esse atributo.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Um valor SQLPOINTER que aponta para a estrutura de contexto.<br /><br /> Somente o Gerenciador de Driver pode chamar um driver **SQLSetStmtAttr** função com esse atributo.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|Um valor SQLULEN que especifica se uma função chamada com uma instrução em que a conexão especificada é executada de forma assíncrona:<br /><br /> SQL_ASYNC_ENABLE_OFF = desabilitar o suporte de nível de execução assíncrona de conexão para operações de instrução (o padrão).<br /><br /> SQL_ASYNC_ENABLE_ON = habilitar o suporte de nível de execução assíncrona de conexão para operações de instrução.<br /><br /> Esse atributo pode ser definido se **SQLGetInfo** com as informações de SQL_ASYNC_MODE tipo retorna SQL_AM_CONNECTION ou SQL_AM_STATEMENT.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|Um valor SQLUINTEGER somente leitura que especifica se preenchimento automático do IPD após uma chamada para **SQLPrepare** tem suporte:<br /><br /> SQL_TRUE = o preenchimento automático do IPD após uma chamada para **SQLPrepare** é suportado pelo driver.<br /><br /> SQL_FALSE = o preenchimento automático do IPD após uma chamada para **SQLPrepare** não tem suporte pelo driver. Servidores que não oferecem suporte a instruções preparadas não poderá preencher o IPD automaticamente.<br /><br /> Se SQL_TRUE for retornado para o atributo de conexão SQL_ATTR_AUTO_IPD, o atributo de instrução SQL_ATTR_ENABLE_AUTO_IPD pode ser definido para ativar ou desativar o preenchimento automático do IPD. Se SQL_ATTR_AUTO_IPD for SQL_FALSE, SQL_ATTR_ENABLE_AUTO_IPD não pode ser definido como SQL_TRUE. O valor padrão de SQL_ATTR_ENABLE_AUTO_IPD é igual ao valor de SQL_ATTR_AUTO_IPD.<br /><br /> Esse atributo de conexão pode ser retornado por **SQLGetConnectAttr** , mas não pode ser definida **SQLSetConnectAttr**.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|Um valor SQLUINTEGER que especifica se deve usar o modo de confirmação automática ou manual de confirmação:<br /><br /> SQL_AUTOCOMMIT_OFF = o driver usa o modo de confirmação manual e o aplicativo deve confirmar ou reverter transações com explicitamente **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = o driver usa modo de confirmação automática. Cada instrução é confirmada imediatamente depois que ele é executado. Esse é o padrão. Qualquer transação aberta sobre a conexão serão confirmadas quando SQL_ATTR_AUTOCOMMIT é definido como SQL_AUTOCOMMIT_ON para alterar do modo de confirmação manual para o modo de confirmação automática.<br /><br /> Para obter mais informações, consulte [modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md). **Importante:** algumas fontes de dados excluir os planos de acesso e feche os cursores para todas as instruções em uma conexão sempre que uma instrução é confirmada; modo de confirmação automática pode fazer com que isso aconteça após cada instrução nonquery é executada ou quando o cursor estiver fechado para uma consulta. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [efeito de transações em cursores e instruções preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md). <br /><br /> Quando um lote é executado no modo de confirmação automática, duas coisas são possíveis. O lote inteiro pode ser tratado como uma unidade de autocommitable ou cada instrução em um lote é tratada como uma unidade de autocommitable. Certas fontes de dados podem dar suporte a ambos esses comportamentos e podem fornecer uma maneira de escolher uma ou outra. É definido pelo driver se um lote é tratado como uma unidade de autocommitable ou se cada instrução individual dentro do lote é autocommitable.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|Um valor SQLUINTEGER de somente leitura que indica o estado da conexão. Se SQL_CD_TRUE, a conexão foi perdida. Se SQL_CD_FALSE, a conexão ainda está ativa.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|Um valor de sqluinteger que corresponde ao número de segundos de espera para qualquer solicitação na conexão seja concluída antes de retornar para o aplicativo. O driver deve retornar SQLSTATE HYT00 (tempo limite expirado) a qualquer momento que ela seja possível tempo limite em uma situação não associada a execução da consulta ou de logon.<br /><br /> Se *ValuePtr* é igual a 0 (o padrão), não há nenhum tempo limite.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|Uma cadeia de caracteres que contém o nome do catálogo a ser usado pela fonte de dados. Por exemplo, no SQL Server, o catálogo é um banco de dados para o driver envia um **USE** *banco de dados* instrução à fonte de dados, onde *banco de dados* é o banco de dados especificado em \* *ValuePtr*. Para um driver de camada única, o catálogo pode ser um diretório para o driver altera seu diretório atual para o diretório especificado em **ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|Um valor SQLPOINTER usado para configurar novamente o token de informações de conexão para o DBC tratar quando [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)do (\**pRating*) parâmetro não for igual a 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN é somente de conjunto. Não é possível usar **SQLGetConnectAttr** ou **SQLGetConnectOption** para recuperar esse valor. O Gerenciador de Driver **SQLSetConnectAttr** não aceitará SQL_ATTR_DBC_INFO_TOKEN, desde que um aplicativo não deve definir esse atributo.<br /><br /> Se um driver retornará SQL_ERROR depois de definir SQL_ATTR_DBC_INFO_TOKEN, a conexão apenas obtido no pool será liberada. O Gerenciador de Driver tentará obter outra conexão do pool. Consulte [desenvolvendo o reconhecimento do Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) para obter mais informações.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Um valor SQLPOINTER que especifica se deve usar o driver ODBC em transações distribuídas coordenadas por serviços de componentes da Microsoft.<br /><br /> Passe um DTC OLE objeto de transação que especifica a transação para exportar para o SQL Server ou SQL_DTC_DONE para encerrar a associação de DTC da conexão.<br /><br /> O cliente chama o método de coordenador de transações distribuídas da Microsoft (MS DTC) OLE itransactiondispenser:: BeginTransaction para iniciar uma transação do MS DTC e criar um objeto de transação do MS DTC que representa a transação. O aplicativo chama SQLSetConnectAttr com a opção SQL_ATTR_ENLIST_IN_DTC para associar o objeto de transação de conexão ODBC. Todas as atividades de banco de dados relacionadas serão executadas sob a proteção da transação do MS DTC. O aplicativo chama SQLSetConnectAttr com SQL_DTC_DONE para encerrar a associação de DTC da conexão. Para obter mais informações, consulte a documentação do MS DTC.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|Um valor de sqluinteger que corresponde ao número de segundos a aguardar uma solicitação de logon concluir antes de retornar ao aplicativo. O padrão é dependente do driver. Se *ValuePtr* é 0, o tempo limite será desabilitado e uma tentativa de conexão aguardará indefinidamente.<br /><br /> Se o tempo limite especificado excede o tempo limite de logon máximo na fonte de dados, o driver substitui esse valor e retornará SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Um valor SQLUINTEGER que determina como são tratados os argumentos de cadeia de caracteres de funções de catálogo.<br /><br /> Se SQL_TRUE, o argumento de cadeia de caracteres de funções de catálogo são tratadas como identificadores. Caso não é significativo. Cadeias de caracteres não delimitados, o driver remove os espaços à direita e a cadeia de caracteres é armazenada em maiusculas. Cadeias de caracteres delimitada, o driver remove espaços à esquerda ou à direita e leva literalmente tudo o que está entre os delimitadores. Se um desses argumentos é definido como um ponteiro nulo, a função retornará SQL_ERROR e SQLSTATE HY009 (uso inválido de ponteiro nulo).<br /><br /> Se SQL_FALSE, os argumentos de cadeia de caracteres de funções de catálogo não são tratadas como identificadores. O caso é significativo. Eles podem conter um padrão de pesquisa de cadeia de caracteres ou não, dependendo do argumento.<br /><br /> O valor padrão é SQL_FALSE.<br /><br /> O *TableType* argumento de **SQLTables**, que usa uma lista de valores, não é afetado por esse atributo.<br /><br /> SQL_ATTR_METADATA_ID também podem ser definidas no nível de instrução. (É o atributo de conexão única que também é um atributo de instrução).<br /><br /> Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Um valor SQLULEN que especifica como o Gerenciador de Driver usa a biblioteca de cursores ODBC:<br /><br /> SQL_CUR_USE_IF_NEEDED = o Gerenciador de Driver usa a biblioteca de cursores ODBC somente se for necessário. Se o driver dá suporte à opção SQL_FETCH_PRIOR na **SQLFetchScroll**, o Gerenciador de Driver usa os recursos de rolagem do driver. Caso contrário, ele usa a biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_ODBC = o Gerenciador de Driver usa a biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_DRIVER = o Gerenciador de Driver usa os recursos de rolagem do driver. Essa é a configuração padrão.<br /><br /> Para obter mais informações sobre a biblioteca de cursores ODBC, consulte [biblioteca de cursores de ODBC apêndice f:](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md). **Aviso:** a biblioteca de cursores será removida em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|Um valor SQLUINTEGER especificando o tamanho do pacote de rede em bytes. **Observação:** várias fontes de dados não suportam essa opção ou somente retorno mas não podem definir o tamanho do pacote de rede. <br /><br /> Se o tamanho especificado excede o tamanho máximo do pacote ou é menor do que o tamanho mínimo do pacote, o driver substitui esse valor e retornará SQLSTATE 01S02 (valor da opção alterado).<br /><br /> Se o aplicativo define o tamanho do pacote depois que uma conexão já estabelecida, o driver retornará SQLSTATE HY011 (atributo não pode ser definido agora).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|Um identificador de janela (HWND).<br /><br /> Se o identificador de janela é um ponteiro nulo, o driver não exibe nenhuma caixa de diálogo.<br /><br /> Se o identificador de janela não é um ponteiro nulo, ele deve ser o identificador da janela pai do aplicativo. Esse é o padrão. O driver usa esse identificador para exibir caixas de diálogo. **Observação:** o atributo de conexão SQL_ATTR_QUIET_MODE não se aplicam a caixas de diálogo exibidas por **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1.0)|Um valor SQLUINTEGER informando o Gerenciador de Driver se deseja executar o rastreamento:<br /><br /> SQL_OPT_TRACE_OFF = rastreamento desativado (padrão)<br /><br /> SQL_OPT_TRACE_ON = rastreamento em<br /><br /> Quando o rastreamento está ativado, o Gerenciador de Driver grava cada chamada de função ODBC para o arquivo de rastreamento. **Observação:** quando o rastreamento está ativado, o Gerenciador de Driver pode retornar SQLSTATE IM013 (erro de arquivo de rastreamento) de qualquer função. <br /><br /> Um aplicativo especifica um arquivo de rastreamento com a opção SQL_ATTR_TRACEFILE. Se o arquivo já existir, o Gerenciador de Driver anexa ao arquivo. Caso contrário, ele cria o arquivo. Se o rastreamento está em e nenhum arquivo de rastreamento tiver sido especificado, o Gerenciador de Driver grava no arquivo SQL. Faça logon no diretório raiz.<br /><br /> Um aplicativo pode definir a variável **ODBCSharedTraceFlag** para habilitar o rastreamento dinamicamente. Em seguida, o rastreamento está habilitado para todos os aplicativos ODBC em execução no momento. Se um aplicativo desativa o rastreamento, ela é desativada para o aplicativo.<br /><br /> Se o **rastreamento** palavra-chave nas informações do sistema é definido como 1 quando um aplicativo chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV, o rastreamento está habilitado para todos identificadores. Ele é habilitado somente para o aplicativo que chamou **SQLAllocHandle**.<br /><br /> Chamando **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_TRACE não requer que o *identificador da conexão* argumento seja válido e não retornará SQL_ERROR se *Identificador da conexão* é NULL. Este atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Uma cadeia de caracteres terminada por caractere nulo que contém o nome do arquivo de rastreamento.<br /><br /> O valor padrão do atributo SQL_ATTR_TRACEFILE for especificado com o **TraceFile** palavra-chave nas informações do sistema. Para obter mais informações, consulte [ODBC subchave](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Chamando **SQLSetConnectAttr** com um *atributo* de sql_attr TRACEFILE não exigem o *identificador da conexão* argumento válido e não retornará SQL_ERROR se *Identificador da conexão* é inválido. Este atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Uma cadeia de caracteres terminada em nulo que contém o nome de uma biblioteca que contém as funções **SQLDriverToDataSource** e **SQLDataSourceToDriver** que o driver acessa para executar tarefas como tradução do conjunto de caracteres. Essa opção pode ser especificado somente se o driver conectou-se à fonte de dados. A configuração deste atributo será mantido em conexões. Para obter mais informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md) e [referência de função de DLL de conversão](../../../odbc/reference/syntax/translation-dll-api-reference.md).|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|Um valor de sinalizador de 32 bits que é passado para a DLL de conversão. Esse atributo pode ser especificado somente se o driver conectou-se à fonte de dados. Para obter informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|Um bitmask de 32 bits que define o nível de isolamento de transação para a conexão atual. Um aplicativo deve chamar **SQLEndTran** para confirmar ou reverter todas as transações abertas em uma conexão, antes de chamar **SQLSetConnectAttr** com essa opção.<br /><br /> Os valores válidos para *ValuePtr* pode ser determinado chamando **SQLGetInfo** com *informação* igual a SQL_TXN_ISOLATION_OPTIONS.<br /><br /> Para obter uma descrição dos níveis de isolamento de transação, consulte a descrição do tipo de informações de SQL_DEFAULT_TXN_ISOLATION no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [níveis de isolamento da transação](../../../odbc/reference/develop-app/transaction-isolation-levels.md).|  
  
 [1] essas funções podem ser chamadas de forma assíncrona somente se o descritor é um descritor de implementação, não um descritor de aplicativo.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

