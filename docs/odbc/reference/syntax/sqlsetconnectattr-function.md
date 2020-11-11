---
description: Função SQLSetConnectAttr
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e6e3e9722510b7a1a563de8546b2e4190696e10
ms.sourcegitcommit: 3bde506b2fa3bc82813dbe658d567b1b9eb4278b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94498449"
---
# <a name="sqlsetconnectattr-function"></a>Função SQLSetConnectAttr
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLSetConnectAttr** define atributos que regem aspectos de conexões.  
  
> [!NOTE]
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um aplicativo ODBC 3 *. x* está trabalhando com um driver ODBC 2 *. x* , consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *Atributo*  
 Entrada Atributo a ser definido, listado em "Comentários".  
  
 *ValuePtr*  
 Entrada Ponteiro para o valor a ser associado ao *atributo*. Dependendo do valor do *atributo* , *ValuePtr* será um valor inteiro sem sinal ou apontará para uma cadeia de caracteres terminada em nulo. Observe que o tipo integral do argumento de *atributo* pode não ter comprimento fixo, consulte a seção de comentários para obter detalhes.  
  
 *StringLength*  
 Entrada Se o *atributo* for um atributo definido pelo ODBC e *ValuePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o comprimento de * *ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se o *atributo* for um atributo definido pelo ODBC e *ValuePtr* for um inteiro, *StringLength* será ignorado.  
  
 Se o *atributo* for um atributo definido por Driver, o aplicativo indicará a natureza do atributo para o Gerenciador de driver, definindo o argumento *StringLength* . *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* for um ponteiro para uma cadeia de caracteres, *StringLength* será o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR ( *Length* ) em *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, *StringLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, o *StringLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLSetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *identificador* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetConnectAttr** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
 O driver pode retornar SQL_SUCCESS_WITH_INFO para fornecer informações sobre o resultado da definição de uma opção.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não oferecia suporte ao valor especificado em *ValuePtr* e substituiu um valor semelhante. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08002|Nome da conexão em uso|O argumento de *atributo* foi SQL_ATTR_ODBC_CURSORS e o driver já estava conectado à fonte de dados.|  
|08003|Conexão não aberta|(DM) foi especificado um valor de *atributo* que exigia uma conexão aberta, mas o *ConnectionHandle* não estava em um estado conectado.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|O argumento de *atributo* foi SQL_ATTR_CURRENT_CATALOG e um conjunto de resultados estava pendente.|  
|25000|Operação ilegal durante uma transação local|Uma conexão estava em uma transação local ao tentar inscrever-se em uma conexão de transação distribuída (DTC) definindo o atributo de conexão SQL_ATTR_ENLIST_IN_DTC.<br /><br /> Uma conexão já está inscrito em um DTC.<br /><br /> Uma conexão foi inscrito em uma conexão de transação distribuída e uma transação local foi iniciada definindo SQL_ATTR_AUTOCOMMIT como SQL_AUTOCOMMIT_OFF.|  
|3D000|Nome de catálogo inválido|O argumento de *atributo* foi SQL_CURRENT_CATALOG e o nome de catálogo especificado era inválido.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer *\* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A **função SQLSetConnectAttr** foi chamada e, antes de concluir a execução, [a função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle* e, em seguida, a função **SQLSetConnectAttr** foi chamada novamente no *ConnectionHandle*.<br /><br /> Ou, a função  **SQLSetConnectAttr** foi chamada e, antes de concluir a execução, **SQLCancelHandle** foi chamado no *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O argumento de *atributo* identificou um atributo de conexão que exigia um valor de cadeia de caracteres e o argumento *ValuePtr* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um *StatementHandle* associado ao *ConnectionHandle* e ainda estava em execução quando **SQLSetConnectAttr** foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute** , **SQLExecDirect** ou **SQLMoreResults** foi chamado para um dos identificadores de instrução associados ao *ConnectionHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) **SQLExecute** , **SQLExecDirect** , **SQLBulkOperations** ou **SQLSetPos** foi chamado para um *StatementHandle* associado ao *ConnectionHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) **SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornou SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|HY011|O atributo não pode ser definido agora|O argumento de *atributo* foi SQL_ATTR_TXN_ISOLATION e uma transação estava aberta.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY024|Valor de atributo inválido|Dado o valor do *atributo* especificado, um valor inválido foi especificado em *ValuePtr*. (O Gerenciador de driver retorna este SQLSTATE somente para atributos de conexão e instrução que aceitam um conjunto discreto de valores, como SQL_ATTR_ACCESS_MODE ou SQL_ATTR_ASYNC_ENABLE. Para todos os outros atributos de instrução e conexão, o driver deve verificar o valor especificado em *ValuePtr*.)<br /><br /> O argumento de *atributo* foi SQL_ATTR_TRACEFILE ou SQL_ATTR_TRANSLATE_LIB e *ValuePtr* era uma cadeia de caracteres vazia.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|*(DM) \* ValuePtr* é uma cadeia de caracteres e o argumento *StringLength* era menor que 0, mas não foi SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o *atributo* de argumento não era válido para a versão do ODBC com suporte do driver.<br /><br /> (DM) o valor especificado para o *atributo* de argumento era um atributo somente leitura.|  
|HY114|O driver não dá suporte à execução de função assíncrona no nível de conexão|(DM) um aplicativo tentou habilitar a execução de função assíncrona com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para um driver que não oferece suporte a operações de conexão assíncronas.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|A biblioteca de cursores e o pool de Driver-Aware não podem ser habilitados ao mesmo tempo|Para obter mais informações, consulte [pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo* de argumento era um atributo de instrução ou conexão ODBC válido para a versão do ODBC com suporte do driver, mas sem suporte do driver.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr** , SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *ConnectionHandle* não oferece suporte à função.|  
|IM009|Não é possível carregar a DLL de tradução|O driver não pôde carregar a DLL de tradução que foi especificada para a conexão. Esse erro só pode ser retornado quando o *atributo* é SQL_ATTR_TRANSLATE_LIB.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
|S1118|O driver não oferece suporte à notificação assíncrona|SQL_ATTR_ASYNC_DBC_EVENT foi definido (após a conexão ter sido feita), mas a notificação assíncrona não é suportada pelo driver.|  
  
 Quando o *atributo* é um atributo de instrução, **SQLSetConnectAttr** pode retornar qualquer sqlstates retornado por **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre atributos de conexão, consulte [atributos de conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Os atributos definidos atualmente e a versão do ODBC em que eles foram introduzidos são mostrados na tabela mais adiante nesta seção; Espera-se que mais atributos sejam definidos para tirar proveito de diferentes fontes de dados. Um intervalo de atributos é reservado pelo ODBC; os desenvolvedores de driver devem reservar valores para seu próprio uso específico de driver de um grupo aberto.  
  
> [!NOTE]
>  A capacidade de definir atributos de instrução no nível de conexão chamando **SQLSetConnectAttr** foi preterida no ODBC 3 *. x*. Os aplicativos ODBC 3 *. x* nunca devem definir atributos de instrução no nível de conexão. Os atributos de instrução ODBC 3 *. x* não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de instrução e podem ser definidos no nível de conexão ou no nível de instrução.  
> 
>  Os drivers ODBC 3 *. x* precisam dar suporte apenas a essa funcionalidade se eles devem funcionar com aplicativos ODBC 2 *. x* que definem as opções de instrução ODBC 2 *. x* no nível de conexão. Para obter mais informações, consulte [mapeamento de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
 Um aplicativo pode chamar **SQLSetConnectAttr** a qualquer momento entre a hora em que a conexão é alocada e liberada. Todos os atributos de conexão e instrução definidos com êxito pelo aplicativo para a conexão persistem até que **SQLFreeHandle** seja chamado na conexão. Por exemplo, se um aplicativo chama **SQLSetConnectAttr** antes de se conectar a uma fonte de dados, o atributo persiste mesmo se **SQLSetConnectAttr** falhar no driver quando o aplicativo se conectar à fonte de dados; se um aplicativo definir um atributo específico do driver, o atributo persiste mesmo que o aplicativo se conecte a um driver diferente na conexão.  
  
 Alguns atributos de conexão podem ser definidos somente antes que uma conexão seja feita; outras podem ser definidas somente depois que uma conexão é estabelecida. A tabela a seguir indica os atributos de conexão que devem ser definidos antes ou depois que uma conexão foi feita. *Indica que* o atributo pode ser definido antes ou após a conexão.  
  
|Atributo|Definir antes ou depois da conexão?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|Você pode usar o|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|Você pode usar o|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|Você pode usar o|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|Você pode usar o|  
|SQL_ATTR_AUTOCOMMIT|[5]|  
|SQL_ATTR_CONNECTION_DEAD|Depois|  
|SQL_ATTR_CONNECTION_TIMEOUT|Você pode usar o|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|Depois|  
|SQL_ATTR_ENLIST_IN_DTC|Depois|  
|SQL_ATTR_LOGIN_TIMEOUT|Antes|  
|SQL_ATTR_METADATA_ID|Você pode usar o|  
|SQL_ATTR_ODBC_CURSORS|Antes|  
|SQL_ATTR_PACKET_SIZE|Antes|  
|SQL_ATTR_QUIET_MODE|Você pode usar o|  
|SQL_ATTR_TRACE|Você pode usar o|  
|SQL_ATTR_TRACEFILE|Você pode usar o|  
|SQL_ATTR_TRANSLATE_LIB|Depois|  
|SQL_ATTR_TRANSLATE_OPTION|Depois|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE e SQL_ATTR_CURRENT_CATALOG podem ser definidos antes ou depois da conexão, dependendo do driver. No entanto, os aplicativos interoperáveis os definem antes de se conectar, pois alguns drivers não dão suporte à alteração deles após a conexão.  
  
 [2] SQL_ATTR_ASYNC_ENABLE deve ser definida antes que haja uma instrução ativa.  
  
 [3] SQL_ATTR_TXN_ISOLATION só poderá ser definida se não houver transações abertas na conexão. Alguns atributos de conexão dão suporte à substituição de um valor semelhante se a fonte de dados não oferecer suporte ao valor especificado em \* *ValuePtr*. Nesses casos, o driver retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valor da opção alterado). Por exemplo, se o *atributo* for SQL_ATTR_PACKET_SIZE e \* *ValuePtr* exceder o tamanho máximo do pacote, o driver substituirá o tamanho máximo. Para determinar o valor substituído, um aplicativo chama **SQLGetConnectAttr**.  
  
 [4] se SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE for definido antes de uma conexão ser aberta, o Gerenciador de driver definirá o atributo do driver quando o driver for carregado durante uma chamada para **SQLBrowseConnect** , **SQLConnect** ou **SQLDriverConnect**. Antes de uma chamada para **SQLBrowseConnect** , **SQLConnect** ou **SQLDriverConnect** , o Gerenciador de driver não sabe a qual driver se conectar e não sabe se o driver dá suporte a operações de conexão assíncronas. Portanto, o Gerenciador de driver sempre retorna SQL_SUCCESS. Mas, caso o driver não ofereça suporte a operações de conexão assíncrona, a chamada para **SQLBrowseConnect** , **SQLConnect** ou **SQLDriverConnect** falhará.  
  
 [5] quando SQL_ATTR_AUTOCOMMIT for definido como FALSE, os aplicativos deverão chamar SQLEndTran (SQL_ROLLBACK) se qualquer API retornar SQL_ERROR para garantir a consistência transacional.  
  
 O formato das informações definidas no buffer \* *ValuePtr* depende do *atributo* especificado. **SQLSetConnectAttr** aceitará informações de atributo em um dos dois formatos diferentes: uma cadeia de caracteres terminada em nulo ou um valor inteiro. O formato de cada um é observado na descrição do atributo. As cadeias de caracteres apontadas pelo argumento *ValuePtr* de **SQLSetConnectAttr** têm um comprimento de *StringLength* bytes.  
  
 O argumento *StringLength* será ignorado se o comprimento for definido pelo atributo, como é o caso de todos os atributos introduzidos no ODBC 2 *. x* ou anterior.  
  
|*Atributo*|Conteúdo do *ValuePtr*|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1,0)|Um valor SQLUINTEGER. SQL_MODE_READ_ONLY é usado pelo driver ou pela fonte de dados como um indicador de que a conexão não é necessária para dar suporte a instruções SQL que causam a ocorrência de atualizações. Esse modo pode ser usado para otimizar as estratégias de bloqueio, o gerenciamento de transações ou outras áreas apropriadas para o driver ou a fonte de dados. O driver não é necessário para impedir que essas instruções sejam enviadas à fonte de dados. O comportamento do driver e da fonte de dados quando solicitado a processar instruções SQL que não são somente leitura durante uma conexão somente leitura é definido pela implementação. SQL_MODE_READ_WRITE é o padrão.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3,8)|Um valor SQLPOINTER que é um manipulador de eventos.<br /><br /> A notificação da conclusão de funções assíncronas é habilitada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_ASYNC_STMT_EVENT e especificando o identificador de evento. **Observação:**  Não há suporte para o método de notificação com a biblioteca de cursores. Um aplicativo receberá uma mensagem de erro se tentar habilitar a biblioteca de cursores via SQLSetConnectAttr, quando o método de notificação estiver habilitado.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3,8)|Um valor SQLUINTEGER que habilita ou desabilita a execução assíncrona de funções selecionadas no identificador de conexão. Para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = habilitar operação assíncrona para funções relacionadas à conexão especificadas.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (padrão) desabilite a operação assíncrona para funções relacionadas à conexão especificadas.<br /><br /> A configuração SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE é sempre síncrona (ou seja, nunca retornará SQL_STILL_EXECUTING).<br /><br /> A execução assíncrona de operações de instrução é habilitada com SQL_ATTR_ASYNC_ENABLE.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3,8)|Um valor SQLPOINTER que aponta para a estrutura de contexto.<br /><br /> Somente o Gerenciador de driver pode chamar a função **SQLSetStmtAttr** de um driver com esse atributo.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3,8)|Um valor SQLPOINTER que aponta para a estrutura de contexto.<br /><br /> Somente o Gerenciador de driver pode chamar a função **SQLSetStmtAttr** de um driver com esse atributo.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3,0)|Um valor SQLULEN que especifica se uma função chamada com uma instrução na conexão especificada é executada de forma assíncrona:<br /><br /> SQL_ASYNC_ENABLE_OFF = desabilitar o suporte à execução assíncrona de nível de conexão para operações de instrução (o padrão).<br /><br /> SQL_ASYNC_ENABLE_ON = habilitar o suporte de execução assíncrona de nível de conexão para operações de instrução.<br /><br /> Esse atributo pode ser definido se **SQLGetInfo** com o tipo de informação SQL_ASYNC_MODE retorna SQL_AM_CONNECTION ou SQL_AM_STATEMENT.|  
|SQL_ATTR_AUTO_IPD (ODBC 3,0)|Um valor SQLUINTEGER somente leitura que especifica se a população automática do IPD após uma chamada para **SQLPrepare** é suportada:<br /><br /> SQL_TRUE = população automática do IPD após uma chamada para **SQLPrepare** é suportada pelo driver.<br /><br /> SQL_FALSE = população automática do IPD após uma chamada para **SQLPrepare** não é suportada pelo driver. Os servidores que não dão suporte a instruções preparadas não poderão preencher automaticamente o IPD.<br /><br /> Se SQL_TRUE for retornado para o atributo de conexão SQL_ATTR_AUTO_IPD, o atributo de instrução SQL_ATTR_ENABLE_AUTO_IPD poderá ser definido para ativar ou desativar a população automática do IPD. Se SQL_ATTR_AUTO_IPD for SQL_FALSE, SQL_ATTR_ENABLE_AUTO_IPD não poderá ser definido como SQL_TRUE. O valor padrão de SQL_ATTR_ENABLE_AUTO_IPD é igual ao valor de SQL_ATTR_AUTO_IPD.<br /><br /> Esse atributo de conexão pode ser retornado por **SQLGetConnectAttr** , mas não pode ser definido por **SQLSetConnectAttr**.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1,0)|Um valor SQLUINTEGER que especifica se o modo de confirmação automática ou de confirmação manual deve ser usado:<br /><br /> SQL_AUTOCOMMIT_OFF = o driver usa o modo de confirmação manual e o aplicativo deve confirmar explicitamente ou reverter transações com **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = o driver usa o modo de confirmação automática. Cada instrução é confirmada imediatamente após ser executada. Este é o padrão. Todas as transações abertas na conexão são confirmadas quando SQL_ATTR_AUTOCOMMIT é definida como SQL_AUTOCOMMIT_ON para alterar do modo de confirmação manual para o modo de confirmação automática.<br /><br /> Para obter mais informações, consulte [modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md). **Importante:**  Algumas fontes de dados excluem os planos de acesso e fecham os cursores de todas as instruções em uma conexão sempre que uma instrução é confirmada; o modo de confirmação automática pode fazer com que isso aconteça depois que cada instrução nonquery é executada ou quando o cursor é fechado para uma consulta. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR em [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [efeito de transações em cursores e instruções](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)preparadas. <br /><br /> Quando um lote é executado no modo de confirmação automática, duas coisas são possíveis. Todo o lote pode ser tratado como uma unidade de confirmação automática, ou cada instrução em um lote é tratada como uma unidade de confirmação automática. Determinadas fontes de dados podem dar suporte a esses dois comportamentos e podem fornecer uma maneira de escolher um ou outro. Ele é definido por driver se um lote é tratado como uma unidade de confirmação automática ou se cada instrução individual dentro do lote é automática de confirmação.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3,5)|Um valor SQLUINTEGER somente leitura que indica o estado da conexão. Se SQL_CD_TRUE, a conexão foi perdida. Se SQL_CD_FALSE, a conexão ainda estará ativa.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3,0)|Um valor SQLUINTEGER que corresponde ao número de segundos a aguardar a conclusão de qualquer solicitação na conexão antes de retornar ao aplicativo. O driver deve retornar SQLSTATE HYT00 (timeout expirado) a qualquer momento que seja possível atingir o tempo limite em uma situação não associada à execução ou ao logon da consulta.<br /><br /> Se *ValuePtr* for igual a 0 (o padrão), não haverá nenhum tempo limite.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2,0)|Uma cadeia de caracteres que contém o nome do catálogo a ser usado pela fonte de dados. Por exemplo, em SQL Server, o catálogo é um banco de dados, de modo que o driver envia uma instrução **use** _Database_ para a fonte de dados, em que *Database* é o banco de dado especificado em \* *ValuePtr*. Para um driver de camada única, o catálogo pode ser um diretório, portanto, o driver altera seu diretório atual para o diretório especificado em * *ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3,8|Um valor SQLPOINTER usado para definir o token de informações de conexão no manipulador DBC quando o parâmetro de [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)( \* *pRating* ) não é igual a 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN é somente definido. Não é possível usar **SQLGetConnectAttr** ou **SQLGetConnectOption** para recuperar esse valor. O **SQLSetConnectAttr** do Gerenciador de driver não aceitará SQL_ATTR_DBC_INFO_TOKEN, pois um aplicativo não deve definir esse atributo.<br /><br /> Se um driver retornar SQL_ERROR após a configuração SQL_ATTR_DBC_INFO_TOKEN, a conexão que acabou de ser obtida do pool será liberada. O Gerenciador de driver tentará então obter outra conexão do pool. Consulte [desenvolvendo Connection-Pool conscientização em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) para obter mais informações.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3,0)|Um valor SQLPOINTER que especifica se o driver ODBC deve ser usado em transações distribuídas coordenadas pelos serviços de componentes da Microsoft.<br /><br /> Passe um objeto de transação OLE DTC que especifica a transação a ser exportada para SQL Server ou SQL_DTC_DONE para encerrar a associação DTC da conexão.<br /><br /> O cliente chama o método OLE ITransactionDispenser:: BeginTransaction do Microsoft Coordenador de Transações Distribuídas (MS DTC) para iniciar uma transação do MS DTC e criar um objeto de transação MS DTC que representa a transação. Em seguida, o aplicativo chama SQLSetConnectAttr com a opção SQL_ATTR_ENLIST_IN_DTC para associar o objeto de transação à conexão ODBC. Todas as atividades de banco de dados relacionadas serão executadas sob a proteção da transação do MS DTC. O aplicativo chama SQLSetConnectAttr com SQL_DTC_DONE para encerrar a associação de DTC da conexão. Para obter mais informações, consulte a documentação do MS DTC.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1,0)|Um valor SQLUINTEGER que corresponde ao número de segundos a aguardar a conclusão de uma solicitação de logon antes de retornar ao aplicativo. O padrão é dependente de driver. Se *ValuePtr* for 0, o tempo limite será desabilitado e uma tentativa de conexão aguardará indefinidamente.<br /><br /> Se o tempo limite especificado exceder o tempo limite máximo de logon na fonte de dados, o driver substituirá esse valor e retornará SQLSTATE 01S02 (valor de opção alterado).|  
|SQL_ATTR_METADATA_ID (ODBC 3,0)|Um valor SQLUINTEGER que determina como os argumentos de cadeia de caracteres das funções de catálogo são tratados.<br /><br /> Se SQL_TRUE, o argumento de cadeia de caracteres das funções de catálogo será tratado como identificadores. O caso não é significativo. Para cadeias de caracteres não delimitadas, o driver remove espaços à direita e a cadeia de caracteres é dobrada em maiúsculas. Para cadeias de caracteres delimitadas, o driver remove espaços à esquerda ou à direita e, literalmente, o que estiver entre os delimitadores. Se um desses argumentos for definido como um ponteiro NULL, a função retornará SQL_ERROR e SQLSTATE HY009 (uso inválido de ponteiro NULL).<br /><br /> Se SQL_FALSE, os argumentos de cadeia de caracteres das funções de catálogo não serão tratados como identificadores. O caso é significativo. Eles podem conter um padrão de pesquisa de cadeia de caracteres ou não, dependendo do argumento.<br /><br /> O valor padrão é SQL_FALSE.<br /><br /> O argumento *TableName* de **SQLTables** , que usa uma lista de valores, não é afetado por esse atributo.<br /><br /> SQL_ATTR_METADATA_ID também pode ser definido no nível de instrução. (É o único atributo de conexão que também é um atributo de instrução.)<br /><br /> Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2,0)|Um valor SQLULEN especificando como o Gerenciador de driver usa a biblioteca de cursores ODBC:<br /><br /> SQL_CUR_USE_IF_NEEDED = o Gerenciador de driver usará a biblioteca de cursores ODBC somente se for necessário. Se o driver der suporte à opção SQL_FETCH_PRIOR no **SQLFetchScroll** , o Gerenciador de driver usará os recursos de rolagem do driver. Caso contrário, ele usará a biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_ODBC = o Gerenciador de driver usa a biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_DRIVER = o Gerenciador de driver usa os recursos de rolagem do driver. Essa é a configuração padrão.<br /><br /> Para obter mais informações sobre a biblioteca de cursores ODBC, consulte o [Apêndice F: ODBC cursor library](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md). **AVISO:**  A biblioteca de cursores será removida em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2,0)|Um valor SQLUINTEGER que especifica o tamanho do pacote de rede em bytes. **Observação:**  Muitas fontes de dados não oferecem suporte a essa opção ou só podem retornar, mas não definir o tamanho do pacote de rede. <br /><br /> Se o tamanho especificado exceder o tamanho máximo do pacote ou for menor do que o tamanho mínimo do pacote, o driver substituirá esse valor e retornará SQLSTATE 01S02 (valor da opção alterado).<br /><br /> Se o aplicativo definir o tamanho do pacote depois que uma conexão já tiver sido feita, o driver retornará SQLSTATE HY011 (o atributo não pode ser definido agora).|  
|SQL_ATTR_QUIET_MODE (ODBC 2,0)|Um identificador de janela (HWND).<br /><br /> Se o identificador de janela for um ponteiro nulo, o driver não exibirá nenhuma caixa de diálogo.<br /><br /> Se o identificador de janela não for um ponteiro nulo, ele deverá ser o identificador de janela pai do aplicativo. Este é o padrão. O driver usa esse identificador para exibir caixas de diálogo. **Observação:**  O atributo de conexão SQL_ATTR_QUIET_MODE não se aplica a caixas de diálogo exibidas por **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1,0)|Um valor SQLUINTEGER informando ao Gerenciador de driver se o rastreamento deve ser realizado:<br /><br /> SQL_OPT_TRACE_OFF = rastreamento desativado (o padrão)<br /><br /> SQL_OPT_TRACE_ON = rastreamento ativado<br /><br /> Quando o rastreamento está ativado, o Gerenciador de driver grava cada chamada de função ODBC para o arquivo de rastreamento. **Observação:**  Quando o rastreamento está ativado, o Gerenciador de driver pode retornar SQLSTATE IM013 (erro de arquivo de rastreamento) de qualquer função. <br /><br /> Um aplicativo especifica um arquivo de rastreamento com a opção SQL_ATTR_TRACEFILE. Se o arquivo já existir, o Gerenciador de driver acrescentará ao arquivo. Caso contrário, ele criará o arquivo. Se o rastreamento estiver ativado e nenhum arquivo de rastreamento tiver sido especificado, o Gerenciador de driver gravará no arquivo SQL. Faça logon no diretório raiz.<br /><br /> Um aplicativo pode definir a variável **ODBCSharedTraceFlag** para habilitar o rastreamento dinamicamente. O rastreamento é então habilitado para todos os aplicativos ODBC em execução no momento. Se um aplicativo desativa o rastreamento, ele é desativado apenas para esse aplicativo.<br /><br /> Se a palavra-chave **trace** nas informações do sistema for definida como 1 quando um aplicativo chamar **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV, o rastreamento será habilitado para todos os identificadores. Ele é habilitado somente para o aplicativo que chamou **SQLAllocHandle**.<br /><br /> Chamar **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_TRACE não exige que o argumento *ConnectionHandle* seja válido e não retornará SQL_ERROR se *ConnectionHandle* for nulo. Esse atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRACEFILE (ODBC 1,0)|Uma cadeia de caracteres terminada em nulo que contém o nome do arquivo de rastreamento.<br /><br /> O valor padrão do atributo SQL_ATTR_TRACEFILE é especificado com a palavra-chave **TraceFile** nas informações do sistema. Para obter mais informações, consulte a [subchave ODBC](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Chamar **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_TRACEFILE não exige que o argumento *ConnectionHandle* seja válido e não retornará SQL_ERROR se *ConnectionHandle* for inválido. Esse atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1,0)|Uma cadeia de caracteres terminada em nulo que contém o nome de uma biblioteca que contém as funções **SQLDriverToDataSource** e **SQLDataSourceToDriver** que o driver acessa para executar tarefas como conversão de conjunto de caracteres. Essa opção pode ser especificada somente se o driver tiver se conectado à fonte de dados. A configuração desse atributo persistirá entre as conexões. Para obter mais informações sobre como converter dados, consulte [DLLs de tradução](../../../odbc/reference/develop-app/translation-dlls.md) e referência de função de DLL de [tradução](../../../odbc/reference/syntax/translation-dll-api-reference.md).|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1,0)|Um valor de sinalizador de 32 bits que é passado para a DLL de tradução. Esse atributo só poderá ser especificado se o driver tiver se conectado à fonte de dados. Para obter informações sobre como converter dados, consulte [DLLs de tradução](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1,0)|Um bitmask de 32 bits que define o nível de isolamento da transação para a conexão atual. Um aplicativo deve chamar **SQLEndTran** para confirmar ou reverter todas as transações abertas em uma conexão, antes de chamar **SQLSetConnectAttr** com essa opção.<br /><br /> Os valores válidos para *ValuePtr* podem ser determinados chamando **SQLGetInfo** com *InfoType* igual a SQL_TXN_ISOLATION_OPTIONS.<br /><br /> Para obter uma descrição dos níveis de isolamento da transação, consulte a descrição do tipo de informação SQL_DEFAULT_TXN_ISOLATION em [níveis de isolamento](../../../odbc/reference/develop-app/transaction-isolation-levels.md)de [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e transação.|  
  
 [1] essas funções podem ser chamadas de forma assíncrona somente se o descritor for um descritor de implementação, não um descritor de aplicativo.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
