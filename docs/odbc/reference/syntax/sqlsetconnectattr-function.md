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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8424462ddde4f99196e26d633fddfa5bb2ed6ee9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301932"
---
# <a name="sqlsetconnectattr-function"></a>Função SQLSetConnectAttr
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLSetConnectAttr** define atributos que regem aspectos das conexões.  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um aplicativo ODBC 3 *.x* estiver trabalhando com um driver ODBC*2.x,* consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *Atributo*  
 [Entrada] Atributo ao conjunto, listado em "Comentários".  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado com *Atributo*. Dependendo do valor de *Atributo,* *ValuePtr* será um valor inteiro não assinado ou apontará para uma seqüência de caracteres com término nulo. Observe que o tipo integral do argumento *Atributo* pode não ser de comprimento fixo, consulte a seção Comentários para obter detalhes.  
  
 *Stringlength*  
 [Entrada] Se *Atributo* for um atributo definido pelo ODBC e *o ValuePtr* aponta para uma seqüência de caracteres ou um buffer binário, esse argumento deve ser o comprimento de **ValuePtr*. Para dados de seqüência de caracteres, este argumento deve conter o número de bytes na seqüência de caracteres.  
  
 Se *Atributo* for um atributo definido pelo ODBC e *o ValuePtr* for um inteiro, *StringLength* será ignorado.  
  
 Se *Atributo* for um atributo definido pelo driver, o aplicativo indicará a natureza do atributo ao Gerenciador de driver, definindo o argumento *StringLength.* *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma seqüência de caracteres, então *StringLength* é o comprimento da seqüência ou SQL_NTS.  
  
-   Se *ValuePtr* for um ponteiro para um buffer binário, o aplicativo coloca o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* em *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma seqüência de caracteres ou uma seqüência binária, então *StringLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, então *StringLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *alça* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLSetConnectAttr** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
 O motorista pode retornar SQL_SUCCESS_WITH_INFO para fornecer informações sobre o resultado da configuração de uma opção.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não suportava o valor especificado no *ValuePtr* e substituiu um valor semelhante. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08002|Nome de conexão em uso|O argumento *atributo* foi SQL_ATTR_ODBC_CURSORS, e o motorista já estava conectado à fonte de dados.|  
|08003|Conexão não aberta|(DM) Foi especificado um valor *de atributo* que exigia uma conexão aberta, mas o *ConnectionHandle* não estava em um estado conectado.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|O argumento *do Atributo* foi SQL_ATTR_CURRENT_CATALOG, e um conjunto de resultados estava pendente.|  
|25000|Operação ilegal em uma transação local|Uma conexão estava em uma transação local enquanto tentava se alistar em uma conexão de transação distribuída (DTC) definindo o atributo de conexão SQL_ATTR_ENLIST_IN_DTC.<br /><br /> Uma conexão já está alistada em um DTC.<br /><br /> Uma conexão foi alistada em uma conexão de transação distribuída e uma transação local foi iniciada definindo SQL_ATTR_AUTOCOMMIT para SQL_AUTOCOMMIT_OFF.|  
|3D000|Nome do catálogo inválido|O argumento *Atributo* foi SQL_CURRENT_CATALOG, e o nome do catálogo especificado era inválido.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função **SQLSetConnectAttr** foi chamada e, antes de ser concluída, a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle*e, em seguida, a função **SQLSetConnectAttr** foi chamada novamente no *ConnectionHandle*.<br /><br /> Ou, a função **SQLSetConnectAttr** foi chamada e, antes de concluir a execução, o **SQLCancelHandle** foi chamado no *ConnectionHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O argumento *Atributo* identificou um atributo de conexão que exigia um valor de seqüência de strings, e o argumento *ValuePtr* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para um *StatementHandle* associado ao *ConnectionHandle* e ainda estava sendo executada quando **o SQLSetConnectAttr** foi chamado.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foi chamado para uma das alças de declaração associadas ao *ConnectionHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para um *StatementHandle* associado ao *ConnectionHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) **O SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes **do SQLBrowseConnect** retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|HY011|Atributo não pode ser definido agora|O argumento *do Atributo* foi SQL_ATTR_TXN_ISOLATION, e uma transação foi aberta.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY024|Valor do atributo inválido|Dado o valor *atributo* especificado, um valor inválido foi especificado no *ValuePtr*. (O Driver Manager retorna este SQLSTATE apenas para atributos de conexão e declaração que aceitam um conjunto discreto de valores, como SQL_ATTR_ACCESS_MODE ou SQL_ATTR_ASYNC_ENABLE. Para todos os outros atributos de conexão e declaração, o driver deve verificar o valor especificado no *ValuePtr*.)<br /><br /> O argumento *Attribute* era SQL_ATTR_TRACEFILE ou SQL_ATTR_TRANSLATE_LIB, e *ValuePtr* era uma seqüência vazia.|  
|HY090|Comprimento de seqüência ou buffer inválido|*(DM) \*ValuePtr* é uma seqüência de caracteres, e o argumento *StringLength* foi menor que 0, mas não foi SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|(DM) O valor especificado para o *atributo argumental* não era válido para a versão do ODBC suportada pelo driver.<br /><br /> (DM) O valor especificado para o *atributo argumentdo* era um atributo somente leitura.|  
|HY114|O driver não suporta a execução de função assíncrona em nível de conexão|(DM) Um aplicativo tentou habilitar a execução de funções assíncronas com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para um driver que não suporta operações de conexão assíncronas.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [A função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|Biblioteca do cursor e pooling com reconhecimento de driver não podem ser ativados ao mesmo tempo|Para obter mais informações, consulte [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo argumentdo* era um atributo de conexão ou declaração ODBC válido para a versão do ODBC suportado pelo driver, mas não foi suportado pelo driver.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *ConnectionHandle* não suporta a função.|  
|IM009|Não é possível carregar dll de tradução|O driver não conseguiu carregar a DLL de tradução especificada para a conexão. Este erro só pode ser retornado quando *Atributo* estiver SQL_ATTR_TRANSLATE_LIB.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
|S1118|O driver não suporta notificação assíncrona|SQL_ATTR_ASYNC_DBC_EVENT foi definido (depois que a conexão foi feita), mas a notificação assíncrona não é suportada pelo motorista.|  
  
 Quando *Atributo* é um atributo de declaração, **SQLSetConnectAttr** pode retornar quaisquer SQLSTATEs retornados pelo **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre atributos de conexão, consulte [Atributos de conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Os atributos atualmente definidos e a versão do ODBC em que foram introduzidos são mostrados na tabela mais tarde nesta seção; espera-se que mais atributos sejam definidos para aproveitar diferentes fontes de dados. Uma série de atributos é reservada pela ODBC; os desenvolvedores de driver devem reservar valores para seu próprio uso específico do driver do Open Group.  
  
> [!NOTE]
>  A capacidade de definir atributos de declaração no nível de conexão, chamando **SQLSetConnectAttr,** foi preterida no ODBC 3 *.x*. Os aplicativos ODBC 3 *.x* nunca devem definir atributos de declaração no nível de conexão. Os atributos de declaração ODBC 3 *.x* não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de declaração e podem ser definidos tanto no nível de conexão quanto no nível de declaração.  
> 
>  Os drivers ODBC 3 *.x* só precisam suportar essa funcionalidade se trabalharem com aplicativos ODBC*2.x* que definem opções de declaração ODBC*2.x* no nível de conexão. Para obter mais informações, consulte [SQLSetConnectOption Mapping](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
  
 Um aplicativo pode chamar **SQLSetConnectAttr** a qualquer momento entre o momento em que a conexão é alocada e liberada. Todos os atributos de conexão e declaração definidos com sucesso pelo aplicativo para a conexão persistem até **que o SQLFreeHandle** seja chamado na conexão. Por exemplo, se um aplicativo chamar **SQLSetConnectAttr** antes de se conectar a uma fonte de dados, o atributo persistirá mesmo se o **SQLSetConnectAttr** falhar no driver quando o aplicativo se conectar à fonte de dados; se um aplicativo definir um atributo específico do driver, o atributo persistirá mesmo que o aplicativo se conecte a um driver diferente na conexão.  
  
 Alguns atributos de conexão só podem ser definidos antes de uma conexão ter sido feita; outros só podem ser definidos depois que uma conexão for feita. A tabela a seguir indica os atributos de conexão que devem ser definidos antes ou depois de uma conexão ter sido feita. *Ou* indica que o atributo pode ser definido antes ou depois da conexão.  
  
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
|SQL_ATTR_CONNECTION_DEAD|After (após)|  
|SQL_ATTR_CONNECTION_TIMEOUT|Você pode usar o|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After (após)|  
|SQL_ATTR_ENLIST_IN_DTC|After (após)|  
|SQL_ATTR_LOGIN_TIMEOUT|Antes de|  
|SQL_ATTR_METADATA_ID|Você pode usar o|  
|SQL_ATTR_ODBC_CURSORS|Antes de|  
|SQL_ATTR_PACKET_SIZE|Antes de|  
|SQL_ATTR_QUIET_MODE|Você pode usar o|  
|SQL_ATTR_TRACE|Você pode usar o|  
|SQL_ATTR_TRACEFILE|Você pode usar o|  
|SQL_ATTR_TRANSLATE_LIB|After (após)|  
|SQL_ATTR_TRANSLATE_OPTION|After (após)|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE e SQL_ATTR_CURRENT_CATALOG podem ser definidos antes ou depois da conexão, dependendo do driver. No entanto, os aplicativos interoperáveis os definem antes de se conectar, pois alguns drivers não suportam alterá-los após a conexão.  
  
 [2] SQL_ATTR_ASYNC_ENABLE deve ser definido antes que haja uma declaração ativa.  
  
 [3] SQL_ATTR_TXN_ISOLATION só pode ser definida se não houver transações abertas na conexão. Alguns atributos de conexão suportam a substituição de um \*valor semelhante se a fonte de dados não suportar o valor especificado no *ValuePtr*. Nesses casos, o motorista retorna SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (Valor da opção alterado). Por exemplo, se O \* *Atributo* for SQL_ATTR_PACKET_SIZE e o *ValuePtr* exceder o tamanho máximo do pacote, o driver substituirá o tamanho máximo. Para determinar o valor substituído, um aplicativo chama **SQLGetConnectAttr**.  
  
 [4] Se SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE for definido antes de uma conexão ser aberta, o Driver Manager definirá o atributo do driver quando o driver estiver carregado durante uma chamada para **SQLBrowseConnect,** **SQLConnect**ou **SQLDriverConnect**. Antes de uma chamada para **SQLBrowseConnect,** **SQLConnect**ou **SQLDriverConnect,** o Driver Manager não sabe a qual driver se conectar e não sabe se o driver suporta operações de conexão assíncronas. Portanto, o Driver Manager sempre retorna SQL_SUCCESS. Mas, caso o driver não suporte operações de conexão assíncrona, a chamada para **SQLBrowseConnect,** **SQLConnect**ou **SQLDriverConnect** falhará.  
  
 [5] Quando SQL_ATTR_AUTOCOMMIT for definida como FALSE, os aplicativos devem ligar para SQLEndTran(SQL_ROLLBACK) se qualquer API retornar SQL_ERROR para garantir a consistência transacional.  
  
 O formato das informações \*definidas no buffer *ValuePtr* depende do *Atributo*especificado . **O SQLSetConnectAttr** aceitará informações de atributos em um dos dois formatos diferentes: uma seqüência de caracteres com término nulo ou um valor inteiro. O formato de cada um é anotado na descrição do atributo. As seqüências de caracteres apontadas pelo argumento *ValuePtr* do **SQLSetConnectAttr** têm um comprimento de *bytes StringLength.*  
  
 O argumento *StringLength* é ignorado se o comprimento for definido pelo atributo, como é o caso de todos os atributos introduzidos no ODBC 2 *.x* ou anteriormente.  
  
|*Atributo*|*Conteúdo ValuePtr*|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|Um valor SQLUINTEGER. SQL_MODE_READ_ONLY é usado pelo driver ou fonte de dados como um indicador de que a conexão não é necessária para suportar instruções SQL que fazem com que as atualizações ocorram. Esse modo pode ser usado para otimizar estratégias de bloqueio, gerenciamento de transações ou outras áreas conforme apropriado ao driver ou fonte de dados. O driver não é obrigado a impedir que tais declarações sejam submetidas à fonte de dados. O comportamento do driver e da fonte de dados quando solicitado para processar instruções SQL que não são somente lidas durante uma conexão somente leitura é definido pela implementação. SQL_MODE_READ_WRITE é o padrão.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|Um valor SQLPOINTER que é uma alça de evento.<br /><br /> A notificação da conclusão das funções assíncronas é ativada ligando para **SQLSetConnectAttr** com o atributo SQL_ATTR_ASYNC_STMT_EVENT e especificando o cabo de evento. **Nota:**  O método de notificação não é suportado com a biblioteca do cursor. Um aplicativo receberá mensagem de erro se tentar ativar a biblioteca do cursor via SQLSetConnectAttr, quando o método de notificação estiver ativado.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|Um valor SQLUINTEGER que habilita ou desativa a execução assíncrona de funções selecionadas na alça de conexão. Para obter mais informações, consulte [Execução Assíncrona (Método de Votação)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = Habilitar operação assíncrona para funções especificadas relacionadas à conexão.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (Padrão) Desativar a operação assíncrona para funções especificadas relacionadas à conexão.<br /><br /> Definir SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE é sempre síncrono (ou seja, nunca voltará SQL_STILL_EXECUTING).<br /><br /> A execução assíncrona das operações de declaração são habilitadas com SQL_ATTR_ASYNC_ENABLE.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Um valor SQLPOINTER que aponta para a estrutura do contexto.<br /><br /> Apenas o Gerenciador de Driver pode chamar a função **SQLSetStmtAttr** de um driver com este atributo.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Um valor SQLPOINTER que aponta para a estrutura do contexto.<br /><br /> Apenas o Gerenciador de Driver pode chamar a função **SQLSetStmtAttr** de um driver com este atributo.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|Um valor SQLULEN que especifica se uma função chamada com uma declaração na conexão especificada é executada de forma assíncrona:<br /><br /> SQL_ASYNC_ENABLE_OFF = Desativar o suporte de execução assíncrona do nível de conexão para operações de declaração (o padrão).<br /><br /> SQL_ASYNC_ENABLE_ON = Habilitar suporte de execução assíncrona ao nível de conexão para operações de declaração.<br /><br /> Esse atributo pode ser definido se **o SQLGetInfo** com o SQL_ASYNC_MODE tipo de informação retorna SQL_AM_CONNECTION ou SQL_AM_STATEMENT.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|Um valor SQLUINTEGER somente leitura que especifica se a população automática do IPD após uma chamada para **SQLPrepare** é suportada:<br /><br /> SQL_TRUE = População automática do IPD após uma chamada para **SQLPrepare** é suportada pelo driver.<br /><br /> SQL_FALSE = População automática do IPD após uma chamada para **SQLPrepare** não é suportada pelo driver. Os servidores que não suportam instruções preparadas não poderão preencher o IPD automaticamente.<br /><br /> Se SQL_TRUE for devolvido para o atributo de conexão SQL_ATTR_AUTO_IPD, o atributo de declaração SQL_ATTR_ENABLE_AUTO_IPD pode ser definido para ativar ou desativar a população automática do IPD. Se SQL_ATTR_AUTO_IPD for SQL_FALSE, SQL_ATTR_ENABLE_AUTO_IPD não pode ser definido como SQL_TRUE. O valor padrão de SQL_ATTR_ENABLE_AUTO_IPD é igual ao valor de SQL_ATTR_AUTO_IPD.<br /><br /> Este atributo de conexão pode ser retornado pelo **SQLGetConnectAttr,** mas não pode ser definido pelo **SQLSetConnectAttr**.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|Um valor SQLUINTEGER que especifica se deve usar o modo de confirmação automática ou manual:<br /><br /> SQL_AUTOCOMMIT_OFF = O driver usa o modo de confirmação manual, e o aplicativo deve confirmar ou reverter explicitamente as transações com **o SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = O motorista usa o modo de confirmação automática. Cada declaração é cometida imediatamente após sua execução. Esse é o padrão. Quaisquer transações abertas na conexão são cometidas quando SQL_ATTR_AUTOCOMMIT está definida para SQL_AUTOCOMMIT_ON mudar do modo de confirmação manual para o modo de confirmação automática.<br /><br /> Para obter mais informações, consulte [O modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md). **Importante:**  Algumas fontes de dados excluem os planos de acesso e fecham os cursores para todas as declarações em uma conexão cada vez que uma declaração é comprometida; o modo autocommit pode fazer com que isso aconteça depois que cada declaração de não consulta for executada ou quando o cursor for fechado para uma consulta. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [effect of Transactions on Cursors and Prepared Statements](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md). <br /><br /> Quando um lote é executado no modo de confirmação automática, duas coisas são possíveis. Todo o lote pode ser tratado como uma unidade auto-compromissada, ou cada declaração em um lote é tratada como uma unidade auto-compromissada. Certas fontes de dados podem suportar esses comportamentos e podem fornecer uma maneira de escolher um ou outro. É definido pelo driver se um lote é tratado como uma unidade auto-compromissada ou se cada declaração individual dentro do lote é auto-comprometida.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|Um valor SQLUINTEGER somente leitura que indica o estado da conexão. Se SQL_CD_TRUE, a conexão foi perdida. Se SQL_CD_FALSE, a conexão ainda está ativa.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|Um valor SQLUINTEGER correspondente ao número de segundos para esperar que qualquer solicitação na conexão seja concluída antes de retornar ao aplicativo. O driver deve retornar SQLSTATE HYT00 (Timeout expirado) sempre que for possível cronometrar em uma situação não associada à execução de consulta ou login.<br /><br /> Se *ValuePtr* for igual a 0 (o padrão), não haverá intervalo.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|Uma seqüência de caracteres contendo o nome do catálogo a ser usado pela fonte de dados. Por exemplo, no SQL Server, o catálogo é um banco de dados, então o driver envia \*uma declaração de banco de _dados_ **USE** para a fonte de dados, onde o banco de *dados* é o banco de dados especificado no *ValuePtr*. Para um driver de nível único, o catálogo pode ser um diretório, de modo que o driver altera seu diretório atual para o diretório especificado em **ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8)|Um valor SQLPOINTER usado para definir o token de informações de conexão na alça DBC quando o parâmetro [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)\**(pRating)* não é igual a 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN é apenas set-set. Não é possível usar **SQLGetConnectAttr** ou **SQLGetConnectOption** para recuperar esse valor. O **SQLSetConnectAttr** do Driver Manager não aceitará SQL_ATTR_DBC_INFO_TOKEN, uma vez que um aplicativo não deve definir esse atributo.<br /><br /> Se um driver retornar SQL_ERROR após a configuração SQL_ATTR_DBC_INFO_TOKEN, a conexão obtida apenas no pool será liberada. O Driver Manager tentará obter outra conexão da piscina. Consulte [O desenvolvimento da conscientização do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) para obter mais informações.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Um valor SQLPOINTER que especifica se deve usar o driver ODBC em transações distribuídas coordenadas pela Microsoft Component Services.<br /><br /> Passe um objeto de transação DTC OLE que especifica a transação para exportar para o SQL Server ou SQL_DTC_DONE para encerrar a associação DTC da conexão.<br /><br /> O cliente chama o Microsoft Distributed Transaction Coordinator (MS DTC) OLE ITransactionDispenser::BeginTransaction method to start a MS DTC transaction and create a MS DTC transaction object that represents the transaction. Em seguida, o aplicativo chama o SQLSetConnectAttr com a opção SQL_ATTR_ENLIST_IN_DTC de associar o objeto de transação à conexão ODBC. Todas as atividades de banco de dados relacionadas serão executadas sob a proteção da transação do MS DTC. O aplicativo chama SQLSetConnectAttr com SQL_DTC_DONE para encerrar a associação de DTC da conexão. Para obter mais informações, consulte a documentação do MS DTC.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|Um valor SQLUINTEGER correspondente ao número de segundos para esperar que uma solicitação de login seja concluída antes de retornar ao aplicativo. O padrão é dependente do motorista. Se *o ValuePtr* for 0, o tempo está desativado e uma tentativa de conexão aguardará indefinidamente.<br /><br /> Se o tempo limite especificado exceder o tempo máximo de login na fonte de dados, o driver substitui esse valor e retorna O SQLSTATE 01S02 (valor da opção alterado).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Um valor SQLUINTEGER que determina como os argumentos de seqüência de funções de catálogo são tratados.<br /><br /> Se SQL_TRUE, o argumento de seqüência de funções de catálogo são tratados como identificadores. O caso não é significativo. Para cordas não limitadas, o driver remove todos os espaços de arrasto e a corda é dobrada para maiúsculas. Para cordas delimitadas, o motorista remove qualquer espaço de liderança ou de trilha e leva literalmente o que está entre os delimitadores. Se um desses argumentos estiver definido como um ponteiro nulo, a função retorna SQL_ERROR e SQLSTATE HY009 (uso inválido do ponteiro nulo).<br /><br /> Se SQL_FALSE, os argumentos de seqüência de funções de catálogo não são tratados como identificadores. O caso é significativo. Eles podem conter um padrão de pesquisa de strings ou não, dependendo do argumento.<br /><br /> O valor padrão é SQL_FALSE.<br /><br /> O argumento *TableType* do **SQLTables**, que leva uma lista de valores, não é afetado por esse atributo.<br /><br /> SQL_ATTR_METADATA_ID também podem ser definidos no nível da declaração. (É o único atributo de conexão que também é um atributo de declaração.)<br /><br /> Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Um valor SQLULEN especificando como o Driver Manager usa a biblioteca do cursor ODBC:<br /><br /> SQL_CUR_USE_IF_NEEDED = O Driver Manager usa a biblioteca do cursor ODBC somente se necessário. Se o driver suportar a opção SQL_FETCH_PRIOR no **SQLFetchScroll,** o Gerenciador de driver saqueia os recursos de rolagem do driver. Caso contrário, ele usa a biblioteca do cursor ODBC.<br /><br /> SQL_CUR_USE_ODBC = O Driver Manager usa a biblioteca do cursor ODBC.<br /><br /> SQL_CUR_USE_DRIVER = O Driver Manager usa os recursos de rolagem do driver. Essa é a configuração padrão.<br /><br /> Para obter mais informações sobre a biblioteca do cursor ODBC, consulte [o apêndice F: ODBC Cursor Library](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md). **Aviso:**  A biblioteca do cursor será removida em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|Um valor SQLUINTEGER especificando o tamanho do pacote de rede em bytes. **Nota:**  Muitas fontes de dados não suportam essa opção ou só podem retornar, mas não definir o tamanho do pacote de rede. <br /><br /> Se o tamanho especificado exceder o tamanho máximo do pacote ou for menor do que o tamanho mínimo do pacote, o driver substituirá esse valor e devolverá O SQLSTATE 01S02 (valor da opção alterado).<br /><br /> Se o aplicativo definir o tamanho do pacote depois que uma conexão já tiver sido feita, o driver retornará SQLSTATE HY011 (Atributo não pode ser definido agora).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|Uma alça de janela (HWND).<br /><br /> Se a alça da janela for um ponteiro nulo, o driver não exibirá nenhuma caixa de diálogo.<br /><br /> Se a alça da janela não for um ponteiro nulo, deve ser a alça da janela pai do aplicativo. Esse é o padrão. O driver usa esta alça para exibir caixas de diálogo. **Nota:**  O atributo de conexão SQL_ATTR_QUIET_MODE não se aplica às caixas de diálogo exibidas pelo **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1.0)|Um valor SQLUINTEGER indize ao Driver Manager se deve realizar o rastreamento:<br /><br /> SQL_OPT_TRACE_OFF = Rastreamento (padrão)<br /><br /> SQL_OPT_TRACE_ON = Rastreamento em<br /><br /> Quando o rastreamento está ligado, o Gerenciador de driver grava cada chamada de função ODBC para o arquivo de rastreamento. **Nota:**  Quando o rastreamento estiver ligado, o Driver Manager pode retornar SQLSTATE IM013 (erro de arquivo de rastreamento) de qualquer função. <br /><br /> Um aplicativo especifica um arquivo de rastreamento com a opção SQL_ATTR_TRACEFILE. Se o arquivo já existir, o Driver Manager anexa ao arquivo. Caso contrário, ele cria o arquivo. Se o rastreamento estiver ligado e nenhum arquivo de rastreamento tiver sido especificado, o Driver Manager será gravado no arquivo SQL. FAÇA login no diretório raiz.<br /><br /> Um aplicativo pode definir a variável **ODBCSharedTraceFlag** para permitir o rastreamento dinamicamente. O rastreamento é então habilitado para todos os aplicativos ODBC em execução atualmente. Se um aplicativo desligar o rastreamento, ele será desligado apenas para esse aplicativo.<br /><br /> Se a palavra-chave **Trace** nas informações do sistema for definida como 1 quando um aplicativo chamar **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV, o rastreamento será ativado para todas as alças. Ele está habilitado apenas para o aplicativo chamado **SQLAllocHandle**.<br /><br /> Chamar **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_TRACE não exige que o argumento *ConnectionHandle* seja válido e não retorne SQL_ERROR se *o ConnectionHandle* for NULL. Este atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Uma seqüência de caracteres com término nulo contendo o nome do arquivo de rastreamento.<br /><br /> O valor padrão do atributo SQL_ATTR_TRACEFILE é especificado com a palavra-chave **TraceFile** nas informações do sistema. Para obter mais informações, consulte [Subchave ODBC](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Chamar **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_ TRACEFILE não exige que o argumento *ConnectionHandle* seja válido e não retornará SQL_ERROR se *o ConnectionHandle* estiver inválido. Este atributo se aplica a todas as conexões.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Uma seqüência de caracteres com término nulo contendo o nome de uma biblioteca contendo as funções **SQLDriverToDataSource** e **SQLDataSourceToDriver** que o driver acessa para executar tarefas como tradução de conjunto de caracteres. Essa opção só pode ser especificada se o driver estiver conectado à fonte de dados. A configuração deste atributo persistirá entre as conexões. Para obter mais informações sobre a tradução de dados, consulte [DLLs de tradução](../../../odbc/reference/develop-app/translation-dlls.md) e [referência de função dll de tradução](../../../odbc/reference/syntax/translation-dll-api-reference.md).|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|Um valor de bandeira de 32 bits que é passado para a tradução DLL. Este atributo só pode ser especificado se o driver estiver conectado à fonte de dados. Para obter informações sobre a tradução de dados, consulte [DLLs de tradução](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|Uma máscara de bitde 32 bits que define o nível de isolamento da transação para a conexão atual. Um aplicativo deve ligar para **o SQLEndTran** para confirmar ou reverter todas as transações abertas em uma conexão, antes de ligar para **o SQLSetConnectAttr** com essa opção.<br /><br /> Os valores válidos para *ValuePtr* podem ser determinados ligando para **SQLGetInfo** com *InfoType* igual a SQL_TXN_ISOLATION_OPTIONS.<br /><br /> Para obter uma descrição dos níveis de isolamento de transações, consulte a descrição do SQL_DEFAULT_TXN_ISOLATION tipo de informação no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [nos níveis de isolamento de transações](../../../odbc/reference/develop-app/transaction-isolation-levels.md).|  
  
 [1] Essas funções só podem ser chamadas assíncronamente se o descritor for um descritor de implementação, não um descritor de aplicativo.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando uma alça|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
