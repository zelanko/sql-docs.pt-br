---
title: Função SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607b0d764a694098a23111e9d7f4ce9755ea982d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301336"
---
# <a name="sqlbrowseconnect-function"></a>Função SQLBrowseConnect
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 O **SQLBrowseConnect** dá suporte a um método iterativo de descoberta e enumeração dos atributos e dos valores de atributo necessários para se conectar a uma fonte de dados. Cada chamada para **SQLBrowseConnect** retorna níveis sucessivos de atributos e valores de atributo. Quando todos os níveis tiverem sido enumerados, uma conexão com a fonte de dados será concluída e uma cadeia de conexão completa será retornada por **SQLBrowseConnect**. Um código de retorno de SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO indica que todas as informações de conexão foram especificadas e o aplicativo agora está conectado à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *Inconnectionstring*  
 Entrada Procure a cadeia de conexão de solicitação (consulte o argumento "*Inconnectionstring* " em "Comentários").  
  
 *StringLength1*  
 Entrada Comprimento de **Inconnectionstring* em caracteres.  
  
 *Outconnectstring*  
 Der Ponteiro para um buffer de caracteres no qual retornar a cadeia de conexão de resultado de procura (consulte o argumento "*Outconnectionstring* " em "comments").  
  
 Se *Outconnectionstring* for NULL, *StringLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *outconnectionstring*.  
  
 *BufferLength*  
 Entrada Comprimento, em caracteres, do buffer **Outconnectstring* .  
  
 *StringLength2Ptr*  
 Der O número total de caracteres (excluindo a terminação nula) disponíveis para \*retornar em *outconnectionstring*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength*, a cadeia de conexão em \* *outconnectionstring* será truncada para *BufferLength* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLBrowseConnect** retorna SQL_ERROR, SQL_SUCCESS_WITH_INFO ou SQL_NEED_DATA, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador de ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBrowseConnect** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|A \* *outconnectstring* do buffer não era grande o suficiente para retornar a cadeia de conexão inteira do resultado da procura, portanto, a cadeia de caracteres foi truncada. O buffer **StringLength2Ptr* contém o comprimento da cadeia de conexão de resultado de procura destruncada. (A função retorna SQL_NEED_DATA.)|  
|01S00|Atributo de cadeia de conexão inválido|Uma palavra-chave de atributo inválida foi especificada na cadeia de conexão de solicitação de procura (*Inconnectionstring*). (A função retorna SQL_NEED_DATA.)<br /><br /> Uma palavra-chave de atributo foi especificada na cadeia de conexão de solicitação de procura (*Inconnectionstring*) que não se aplica ao nível de conexão atual. (A função retorna SQL_NEED_DATA.)|  
|01S02|Valor alterado|O driver não oferecia suporte ao valor especificado do argumento *ValuePtr* em **SQLSetConnectAttr** e substituiu um valor semelhante. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de estabelecer conexão|O driver não pôde estabelecer uma conexão com a fonte de dados.|  
|08002|Nome da conexão em uso|(DM) a conexão especificada já foi usada para estabelecer uma conexão com uma fonte de dados e a conexão foi aberta.|  
|08004|O servidor rejeitou a conexão|A fonte de dados rejeitou o estabelecimento da conexão para motivos definidos pela implementação.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver estava tentando se conectar falhou antes da função concluir o processamento.|  
|28000|Especificação de autorização inválida|O identificador de usuário ou a cadeia de caracteres de autorização ou ambos, conforme especificado na cadeia de conexão de solicitação de procura (*Inconnectionstring*), violadas restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) o Gerenciador de driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.<br /><br /> O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|Uma operação assíncrona foi cancelada chamando a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md). Em seguida, a função original foi chamada novamente no *ConnectionHandle*.<br /><br /> Uma operação foi cancelada chamando **SQLCancelHandle** no *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *StringLength1* era menor que 0 e não era igual a SQL_NTS.<br /><br /> (DM) o valor especificado para o argumento *BufferLength* era menor que 0.|  
|HY114|O driver não dá suporte à execução de função assíncrona de nível de conexão|(DM) o aplicativo habilitou a operação assíncrona no identificador de conexão antes de fazer a conexão. No entanto, o driver não oferece suporte à operação assíncrona no identificador de conexão.|  
|HYT00|Tempo limite esgotado|O período de tempo limite de logon expirou antes da conclusão da conexão com a fonte de dados. O período de tempo limite é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver correspondente ao nome da fonte de dados especificado não oferece suporte à função.|  
|IM002|Fonte de dados não encontrada e nenhum driver padrão especificado|(DM) o nome da fonte de dados especificado na cadeia de conexão da solicitação de procura (*Inconnectionstring*) não foi encontrado nas informações do sistema, nem há uma especificação de driver padrão.<br /><br /> (DM) a fonte de dados ODBC e as informações de driver padrão não foram encontradas nas informações do sistema.|  
|IM003|Não foi possível carregar o driver especificado|(DM) o driver listado na especificação de fonte de dados nas informações do sistema ou especificado pela palavra-chave do **Driver** não foi encontrado ou não pôde ser carregado por algum outro motivo.|  
|IM004|Falha no **SQLAllocHandle** do Driver no _ENV de SQL_HANDLE|(DM) durante **SQLBrowseConnect**, o Gerenciador de driver chamou a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_ENV e o driver retornou um erro.|  
|IM005|Falha no **SQLAllocHandle** do Driver em SQL_HANDLE_DBC|(DM) durante **SQLBrowseConnect**, o Gerenciador de driver chamou a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_DBC e o driver retornou um erro.|  
|IM006|Falha no **SQLSetConnectAttr** do driver|(DM) durante **SQLBrowseConnect**, o Gerenciador de driver chamou a função **SQLSetConnectAttr** do driver e o driver retornou um erro.|  
|IM009|Não é possível carregar a DLL de tradução|O driver não pôde carregar a DLL de tradução que foi especificada para a fonte de dados ou para a conexão.|  
|IM010|O nome da fonte de dados é muito longo|(DM) o valor do atributo para a palavra-chave DSN foi maior do que SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nome de driver muito longo|(DM) o valor do atributo para a palavra-chave do DRIVER tinha mais de 255 caracteres.|  
|IM012|Erro de sintaxe de palavra-chave do DRIVER|(DM) o par de palavra-chave-valor da palavra-chave do DRIVER continha um erro de sintaxe.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o driver e o aplicativo|(DM) 32-o aplicativo de bits usa um DSN que se conecta a um driver de 64 bits; ou vice-versa.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
|S1118|O driver não oferece suporte à notificação assíncrona|Quando o driver não dá suporte à notificação assíncrona, não é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>Argumento inconnectionstring  
 Uma cadeia de conexão de solicitação de procura tem a seguinte sintaxe:  
  
 *Connection-String* :: = *Attribute*[`;`] &#124; *attribute* `;` *conexão de atributo-cadeia de caracteres*;<br>
 *atributo* :: = *atributo-palavra-chave*`=`*atributo-valor* &#124; `DRIVER=`[`{`]*atributo-valor*[`}`]<br>
 *atributo-palavra-chave* : `DSN` : `UID` = `PWD` &#124; &#124; &#124; o driver-a *palavra-chave-atributo-defined*<br>
 *atributo-valor* :: = *cadeia de caracteres de caractere*<br>
 *Driver-definido-atributo-palavra-chave* :: = *identificador*<br>
  
 em que *cadeia de caracteres de caractere* tem zero ou mais caracteres; o *identificador* tem um ou mais caracteres; *atributo-a palavra-chave* não diferencia maiúsculas de minúsculas; *atributo-valor* pode diferenciar maiúsculas de minúsculas; e o valor da palavra-chave **DSN** não consiste exclusivamente em espaços em branco. Devido à cadeia de conexão e à gramática de arquivos de inicialização, às palavras-chave e aos valores de atributo que contêm os caracteres **[]{}(),;? = \*! @** deve ser evitado. Devido à gramática nas informações do sistema, as palavras-chave e os nomes de fonte de dados não podem conter\\o caractere de barra invertida (). Para um ODBC 2. Driver *x* , chaves são necessárias em relação ao valor do atributo para a palavra-chave do driver.  
  
 Se qualquer palavra-chave for repetida na cadeia de conexão de solicitação de procura, o driver usará o valor associado à primeira ocorrência da palavra-chave. Se as palavras-chave **DSN** e **Driver** estiverem incluídas na mesma cadeia de conexão de solicitação de procura, o Gerenciador de driver e o driver usarão a palavra-chave que aparece primeiro.  
  
 Para obter informações sobre como um aplicativo escolhe uma fonte de dados ou driver, consulte [escolhendo uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>Argumento outconnectionstring  
 A cadeia de conexão procurar resultado é uma lista de atributos de conexão. Um atributo de conexão consiste em uma palavra-chave de atributo e um valor de atributo correspondente. A cadeia de caracteres de conexão procurar resultado tem a seguinte sintaxe:  
  
 *Connection-String* :: = *Attribute*[`;`] &#124; *attribute* `;` *cadeia de conexão de* atributo<br>
 *atributo::* = [`*`]*atributo-atributo-palavra-chave*`=`*-valor*<br>
 *atributo-palavra-chave* :: = *ODBC-atributo-palavra-chave* &#124; *Driver-definido-atributo-palavra-chave*<br>
 *ODBC-Attribute-palavra* -chave`UID` = `PWD`{&#124;} [`:`*localizador identificador*] *Driver-definido-atributo-de-palavra-chave* :: = *identificador*[`:`*localizador*] *atributo-valor* :: = `{` *atributo-valor-lista* `}` &#124; `?` (as chaves são literais; elas são retornadas pelo driver.)<br>
 *atributo-valor-lista* :: = *Character-String* [`:`*localizada-Character String*] &#124; *caractere-String* [`:`*localizada-Character String*] `,` *atributo-Value-List*<br>
  
 onde *a cadeia* de caracteres e a *cadeia de caracteres localizadas* têm zero ou mais caracteres; o *identificador* e o *identificador localizado* têm um ou mais caracteres; *atributo-a palavra-chave* não diferencia maiúsculas de minúsculas; e o *atributo-valor* pode diferenciar maiúsculas de minúsculas. Devido à cadeia de conexão e à gramática do arquivo de inicialização, palavras-chave, identificadores localizados e valores de atributo que contêm os caracteres **[]{}(),;? = \*! @** deve ser evitado. Devido à gramática nas informações do sistema, as palavras-chave e os nomes de fonte de dados não podem conter\\o caractere de barra invertida ().  
  
 A sintaxe da cadeia de conexão procurar resultado é usada de acordo com as seguintes regras semânticas:  
  
-   Se um asterisco (\*) precede uma *palavra-chave de atributo*, o *atributo* é opcional e pode ser omitido na próxima chamada para **SQLBrowseConnect**.  
  
-   As palavras-chave do atributo **UID** e **pwd** têm o mesmo significado definido em **SQLDriverConnect**.  
  
-   Uma *palavra-chave definida pelo driver* nomeia o tipo de atributo para o qual um valor de atributo pode ser fornecido. Por exemplo, pode ser **servidor**, **banco de dados**, **host**ou **DBMS**.  
  
-   As palavras-chave de *atributo e ODBC-Attribute-* *keysão uma* versão localizada ou amigável do usuário da palavra-chave. Isso pode ser usado por aplicativos como um rótulo em uma caixa de diálogo. No entanto, **UID**, **pwd**ou o *identificador* só deve ser usado ao passar uma cadeia de caracteres de solicitação de procura para o driver.  
  
-   A {*atributo-valor-List*} é uma enumeração de valores reais válidos para a *palavra-chave Attribute*correspondente. Observe que as chaves ({}) não indicam uma lista de opções; Eles são retornados pelo driver. Por exemplo, pode ser uma lista de nomes de servidor ou uma lista de nomes de banco de dados.  
  
-   Se o *atributo-Value* for um ponto de interrogação único (?), um único valor corresponde à *palavra-chave Attribute*. Por exemplo, UID = JohnS; PWD = Sesame.  
  
-   Cada chamada para **SQLBrowseConnect** retorna apenas as informações necessárias para atender ao próximo nível do processo de conexão. O driver associa informações de estado com o identificador de conexão para que o contexto sempre possa ser determinado em cada chamada.  
  
## <a name="using-sqlbrowseconnect"></a>Usando SQLBrowseConnect  
 **SQLBrowseConnect** requer uma conexão alocada. O Gerenciador de driver carrega o driver que foi especificado em ou que corresponde ao nome da fonte de dados especificado na cadeia de conexão inicial da solicitação de procura; para obter informações sobre quando isso ocorre, consulte a seção "Comentários" na [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). O driver pode estabelecer uma conexão com a fonte de dados durante o processo de navegação. Se **SQLBrowseConnect** retornar SQL_ERROR, as conexões pendentes serão encerradas e a conexão será retornada a um estado não conectado.  
  
> [!NOTE]  
>  **SQLBrowseConnect** não dá suporte ao pool de conexões. Se **SQLBrowseConnect** for chamado enquanto o pool de conexões estiver habilitado, SQLState HY000 (erro geral) será retornado.  
  
 Quando **SQLBrowseConnect** é chamado pela primeira vez em uma conexão, a cadeia de conexão da solicitação de procura deve conter a palavra-chave **DSN** ou a palavra-chave do **Driver** . Se a cadeia de conexão da solicitação de procura contiver a palavra-chave **DSN** , o Gerenciador de driver localizará uma especificação de fonte de dados correspondente nas informações do sistema:  
  
-   Se o Gerenciador de driver encontrar a especificação de fonte de dados correspondente, ele carregará a DLL do driver associado; o driver pode recuperar informações sobre a fonte de dados das informações do sistema.  
  
-   Se o Gerenciador de driver não encontrar a especificação de fonte de dados correspondente, ele localizará a especificação de fonte de dados padrão e carregará a DLL do driver associado; o driver pode recuperar informações sobre a fonte de dados padrão das informações do sistema. "DEFAULT" é passado para o driver para o DSN.  
  
-   Se o Gerenciador de driver não encontrar a especificação de fonte de dados correspondente e não houver nenhuma especificação de fonte de dados padrão, ele retornará SQL_ERROR com SQLSTATE IM002 (fonte de dados não encontrada e nenhum driver padrão especificado).  
  
 Se a cadeia de conexão da solicitação de procura contiver a palavra-chave **Driver** , o Gerenciador de driver carregará o driver especificado; Ele não tenta localizar uma fonte de dados nas informações do sistema. Como a palavra-chave do **Driver** não usa informações das informações do sistema, o driver deve definir palavras-chaves suficientes para que um driver possa se conectar a uma fonte de dados usando apenas as informações nas cadeias de conexão da solicitação de procura.  
  
 Em cada chamada para **SQLBrowseConnect**, o aplicativo especifica os valores de atributo de conexão na cadeia de conexão de solicitação de procura. O driver retorna níveis sucessivos de atributos e valores de atributo na cadeia de conexão de resultado de procura; Ele retornará SQL_NEED_DATA contanto que haja atributos de conexão que ainda não tenham sido enumerados na cadeia de conexão de solicitação de procura. O aplicativo usa o conteúdo da cadeia de conexão de resultado de procura para criar a cadeia de conexão de solicitação de procura para a próxima chamada para **SQLBrowseConnect**. Todos os atributos obrigatórios (aqueles não precedidos por um asterisco no argumento *Outconnectionstring* ) devem ser incluídos na próxima chamada para **SQLBrowseConnect**. Observe que o aplicativo não pode usar o conteúdo das cadeias de conexão do resultado de procura anterior ao criar a cadeia de conexão da solicitação de procura atual; ou seja, não é possível especificar valores diferentes para os atributos definidos nos níveis anteriores.  
  
 Quando todos os níveis de conexão e seus atributos associados tiverem sido enumerados, o driver retornará SQL_SUCCESS, a conexão com a fonte de dados será concluída e uma cadeia de conexão completa será retornada ao aplicativo. A cadeia de conexão é adequada para uso, em conjunto com **SQLDriverConnect**, com a opção SQL_DRIVER_NOPROMPT para estabelecer outra conexão. A cadeia de conexão completa não pode ser usada em outra chamada para **SQLBrowseConnect**; no entanto; Se **SQLBrowseConnect** fossem chamadas novamente, toda a sequência de chamadas teria de ser repetida.  
  
 **SQLBrowseConnect** também retornará SQL_NEED_DATA se houver erros recuperáveis e não fatais durante o processo de procura; por exemplo, uma senha inválida ou palavra-chave de atributo fornecida pelo aplicativo. Quando SQL_NEED_DATA é retornado e a cadeia de conexão do resultado da procura é inalterada, ocorreu um erro e o aplicativo pode chamar **SQLGetDiagRec** para retornar o SQLSTATE para erros de tempo de procura. Isso permite que o aplicativo corrija o atributo e continue a navegação.  
  
 Um aplicativo pode encerrar o processo de procura a qualquer momento chamando **SQLDisconnect**. O driver encerrará todas as conexões pendentes e retornará a conexão a um estado não conectado.  
  
 Se as operações assíncronas estiverem habilitadas no identificador de conexão, **SQLBrowseConnect** também poderá retornar SQL_STILL_EXECUTING. Quando ele retorna SQL_NEED_DATA, um aplicativo deve usar **SQLDisconnect** para cancelar o processo de procura. Se **SQLBrowseConnect** retornar SQL_STILL_EXECUTING, um aplicativo deverá usar **SQLCancelHandle** para cancelar a operação em andamento. Chamar **SQLCancelHandle** depois que a função retorna SQL_NEED_DATA não tem nenhum efeito.  
  
 Para obter mais informações, consulte [conectando-se com SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Se um driver oferecer suporte a **SQLBrowseConnect**, a seção de palavra-chave do driver nas informações do sistema para o driver deverá conter a palavra-chave **ConnectFunctions** com o terceiro conjunto de caracteres como "Y".  
  
## <a name="code-example"></a>Exemplo de código  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à `Trusted_Connection=yes` autenticação do Windows, especifique o lugar das informações de ID de usuário e senha na cadeia de conexão.  
  
 No exemplo a seguir, um aplicativo chama **SQLBrowseConnect** repetidamente. Cada vez que **SQLBrowseConnect** retorna SQL_NEED_DATA, ele passa informações sobre os dados de que precisa \*em *outconnectionstring*. O aplicativo passa *Outconnectstring* para sua rotina **GetUserInput** (não mostrada). O **GetUserInput** analisa as informações, cria e exibe uma caixa de diálogo e retorna as informações inseridas pelo usuário em \* *inconnectionstring*. O aplicativo passa as informações do usuário para o driver na próxima chamada para **SQLBrowseConnect**. Depois que o aplicativo tiver fornecido todas as informações necessárias para que o driver se conecte à fonte de dados, **SQLBrowseConnect** retornará SQL_SUCCESS e o aplicativo continuará.  
  
 Para obter um exemplo mais detalhado de como se conectar a um driver de SQL Server chamando **SQLBrowseConnect**, consulte [SQL Server exemplo de navegação](../../../odbc/reference/develop-app/sql-server-browsing-example.md).  
  
 Por exemplo, para se conectar às vendas da fonte de dados, as ações a seguir podem ocorrer. Primeiro, o aplicativo passa a seguinte cadeia de caracteres para **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 O Gerenciador de driver carrega o driver associado às vendas da fonte de dados. Em seguida, ele chama a função **SQLBrowseConnect** do driver com os mesmos argumentos recebidos do aplicativo. O driver retorna a seguinte cadeia de caracteres em **Outconnectionstring*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 O aplicativo passa essa cadeia de caracteres para sua rotina **GetUserInput** , que cria uma caixa de diálogo que solicita ao usuário que selecione o servidor vermelho, azul ou verde e insira uma ID de usuário e senha. A rotina passa as seguintes informações especificadas pelo usuário de volta \*em *inconnectionstring*, que o aplicativo passa para **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 O **SQLBrowseConnect** usa essas informações para se conectar ao servidor vermelho como Smith com a senha Sesame e, em seguida, retorna a seguinte cadeia de caracteres em **outconnectionstring*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 O aplicativo passa essa cadeia de caracteres para sua rotina **GetUserInput** , que cria uma caixa de diálogo que solicita ao usuário para selecionar um banco de dados. O usuário seleciona empdata e o aplicativo chama **SQLBrowseConnect** uma hora final com esta cadeia de caracteres:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Esta é a informação final que o driver precisa para se conectar à fonte de dados; **SQLBrowseConnect** retorna SQL_SUCCESS e **outconnectstring* contém a cadeia de conexão concluída:  
  
```cpp  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador de conexão|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectando de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma cadeia de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando descrições e atributos de driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberando um identificador de conexão|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
