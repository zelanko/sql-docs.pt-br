---
title: Função SQLBrowseConnect | Microsoft Docs
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
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66daf3ce016b8688ada1d584865a97675a7dbc01
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922901"
---
# <a name="sqlbrowseconnect-function"></a>Função SQLBrowseConnect
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLBrowseConnect** oferece suporte a um método iterativo de descoberta e ao enumerar os atributos e valores de atributo necessários para se conectar a uma fonte de dados. Cada chamada para **SQLBrowseConnect** retorna níveis sucessivos de atributos e valores de atributo. Quando todos os níveis foram enumerados, uma conexão à fonte de dados é concluída e uma cadeia de caracteres de conexão completa é retornada por **SQLBrowseConnect**. Um código de retorno de SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO indica que todas as informações de conexão foi especificadas e o aplicativo agora está conectado à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador da conexão*  
 [Entrada] Identificador de Conexão.  
  
 *InConnectionString*  
 [Entrada] Procure a cadeia de caracteres de conexão de solicitação (consulte "*InConnectionString* argumento" em "Comentários").  
  
 *StringLength1*  
 [Entrada] Comprimento de **InConnectionString* em caracteres.  
  
 *OutConnectionString*  
 [Saída] Ponteiro para um buffer de caractere no qual retornar a cadeia de caracteres de conexão de resultado de procura (consulte "*OutConnectionString* argumento" em "Comentários").  
  
 Se *OutConnectionString* for NULL, *StringLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere null de terminação para dados de caractere) disponível no buffer de retorno apontada pelo *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Comprimento em caracteres, do **OutConnectionString* buffer.  
  
 *StringLength2Ptr*  
 [Saída] O número total de caracteres (exceto null de terminação) disponíveis para retornar em \* *OutConnectionString*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength*, a cadeia de caracteres de conexão em \* *OutConnectionString* será truncado para  *BufferLength* menos o comprimento de um caractere null de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLBrowseConnect** retorna SQL_ERROR, SQL_SUCCESS_WITH_INFO ou SQL_NEED_DATA, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* sql_handle_stmt e um *identificador do identificador da conexão*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBrowseConnect** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *OutConnectionString* não era grande o suficiente para retornar a cadeia de caracteres de conexão resultado procurar inteira, para que a cadeia de caracteres foi truncada. O buffer **StringLength2Ptr* contém o comprimento da cadeia de caracteres de conexão de resultados completo procurar. (A função retornará SQL_NEED_DATA.)|  
|01S00|Atributo de cadeia de caracteres de conexão inválido|Uma palavra-chave de atributo inválido foi especificada na cadeia de conexão de solicitação de procura (*InConnectionString*). (A função retornará SQL_NEED_DATA.)<br /><br /> Uma palavra-chave de atributo foi especificada na cadeia de conexão de solicitação de procura (*InConnectionString*) que não se aplica ao nível atual da conexão. (A função retornará SQL_NEED_DATA.)|  
|01S02|Valor foi alterado|O driver não oferecia suporte para o valor especificado do *ValuePtr* argumento **SQLSetConnectAttr** e substituído, um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08001|Não é possível estabelecer a conexão do cliente|O driver não pôde estabelecer uma conexão com a fonte de dados.|  
|08002|Nome da Conexão em uso|(DM) a conexão especificada já tenha sido usada para estabelecer uma conexão com uma fonte de dados, e a conexão foi aberta.|  
|08004|O servidor recusou a conexão|A fonte de dados rejeitados o estabelecimento da conexão por motivos de implementação definida.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver estava tentando conectar-se antes do processamento da função foi concluída.|  
|28000|Especificação de autorização inválida|O identificador de usuário ou a cadeia de caracteres de autorização ou ambos, como especificado em Procurar solicitar a cadeia de caracteres de conexão (*InConnectionString*), violou as restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O Gerenciador de Driver (DM) não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.<br /><br /> O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|Uma operação assíncrona foi cancelada chamando [SQLCancelHandle função](../../../odbc/reference/syntax/sqlcancelhandle-function.md). Em seguida, a função original foi chamada novamente no *identificador da conexão*.<br /><br /> Uma operação foi cancelada chamando **SQLCancelHandle** no *identificador da conexão* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona (não la) foi chamada para o *identificador da conexão* e ainda estava em execução quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *StringLength1* menor que 0 e não era igual a SQL_NTS.<br /><br /> (DM) o valor especificado para o argumento *BufferLength* era menor do que 0.|  
|HY114|Driver não oferece suporte à execução de função assíncrona de nível de conexão|(DM) o aplicativo ativado a operação assíncrona no identificador da conexão antes de fazer a conexão. No entanto, o driver não oferece suporte a operação assíncrona no identificador de conexão.|  
|HYT00|Tempo limite esgotado|O período de tempo limite de logon expirou antes da conexão à fonte de dados foi concluída. O período de tempo limite é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver correspondente ao nome de fonte de dados especificado não oferece suporte para a função.|  
|IM002|Fonte de dados não encontrado e nenhum driver padrão especificado|Nome especificado na cadeia de conexão de solicitação de procura da fonte de dados (DM) (*InConnectionString*) não foi encontrado nas informações do sistema, nem houve uma especificação de driver padrão.<br /><br /> (DM) ODBC dados padrão e fonte de informações sobre o driver não pôde ser encontrado nas informações do sistema.|  
|IM003|Não foi possível carregar o driver especificado|(DM), o driver listados na especificação de fonte de dados nas informações do sistema ou especificado pelo **DRIVER** palavra-chave não foi encontrado ou não pôde ser carregado por algum outro motivo.|  
|IM004|Do driver **SQLAllocHandle** em _ENV SQL_HANDLE falhado|(DM) durante **SQLBrowseConnect**, o Gerenciador de Driver chamado o driver **SQLAllocHandle** funcionar com um *HandleType* SQL_HANDLE_ENV e o driver retornou um erro.|  
|IM005|Do driver **SQLAllocHandle** em SQL_HANDLE_DBC falhado|(DM) durante **SQLBrowseConnect**, o Gerenciador de Driver chamado o driver **SQLAllocHandle** funcionar com um *HandleType* SQL_HANDLE_DBC e o driver retornou um erro.|  
|IM006|Do driver **SQLSetConnectAttr** falha|(DM) durante **SQLBrowseConnect**, o Gerenciador de Driver chamado o driver **SQLSetConnectAttr** função e o driver retornaram um erro.|  
|IM009|Não é possível carregar a DLL de conversão|O driver não pôde carregar a DLL que foi especificada para a fonte de dados ou para a conexão de conversão.|  
|IM010|Nome de fonte de dados muito longo|O valor de atributo para a palavra-chave DSN de (DM) foi mais de SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nome do driver muito longo|(DM) o valor de atributo para a palavra-chave DRIVER tinha mais de 255 caracteres.|  
|IM012|Erro de sintaxe da palavra-chave de DRIVER|(DM) o par de valor de palavra-chave para a palavra-chave DRIVER continha um erro de sintaxe.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o Driver e o aplicativo|Aplicativo de 32 bits (DM) usa um DSN que se conectar a um driver de 64 bits. ou vice-versa.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
|S1118|Driver não dá suporte a notificação assíncrona|Quando o driver não dá suporte a notificação assíncrona, você não pode definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>Argumento InConnectionString  
 Uma cadeia de caracteres de conexão de solicitação de navegação tem a seguinte sintaxe:  
  
 *connection-string* ::= *attribute*[`;`] &#124; *attribute* `;` *connection-string*;<br>
 *attribute* ::= *attribute-keyword*`=`*attribute-value* &#124; `DRIVER=`[`{`]*attribute-value*[`}`]<br>
 *attribute-keyword* ::= `DSN` &#124; `UID` &#124; `PWD` &#124; *driver-defined-attribute-keyword*<br>
 *attribute-value* ::= *character-string*<br>
 *driver-defined-attribute-keyword* ::= *identifier*<br>
  
 onde *cadeia de caracteres* tem zero ou mais caracteres; *identificador* tem um ou mais caracteres; *palavra-chave de atributo* não diferencia maiusculas de minúsculas; *atributo-valor* pode diferenciar maiusculas de minúsculas; e o valor da **DSN** palavra-chave não ser formado apenas por espaços em branco. Devido à conexão cadeia de caracteres e inicialização gramática, palavras-chave e atributo valores do arquivo que contenha os caracteres **[]{}(),? \*=! @** devem ser evitadas. Devido a gramática nas informações do sistema, os nomes de fontes de dados e palavras-chave não podem conter uma barra invertida (\\) caracteres. Para ODBC 2. *x* driver, chaves são necessárias ao redor do valor de atributo para a palavra-chave DRIVER.  
  
 Se quaisquer palavras-chave é repetidos na cadeia de conexão de solicitação de procura, o driver usará o valor associado com a primeira ocorrência da palavra-chave. Se o **DSN** e **DRIVER** palavras-chave são incluídas na mesma cadeia de conexão de solicitação de procura, o Gerenciador de Driver e o driver usam a palavra-chave aparece primeiro.  
  
 Para obter informações sobre como um aplicativo escolhe uma fonte de dados ou driver, consulte [escolhendo uma fonte de dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>Argumento OutConnectionString  
 A cadeia de caracteres de conexão de resultado de procura é uma lista de atributos de conexão. Um atributo de conexão consiste em uma palavra-chave do atributo e um valor de atributo correspondente. A cadeia de caracteres de conexão de resultado de procurar tem a seguinte sintaxe:  
  
 *connection-string* ::= *attribute*[`;`] &#124; *attribute* `;` *connection-string*<br>
 *attribute* ::= [`*`]*attribute-keyword*`=`*attribute-value*<br>
 *attribute-keyword* ::= *ODBC-attribute-keyword* &#124; *driver-defined-attribute-keyword*<br>
 *ODBC-attribute-keyword* = {`UID` &#124; `PWD`}[`:`*localized-identifier*] *driver-defined-attribute-keyword* ::= *identifier*[`:`*localized-identifier*] *attribute-value* ::= `{` *attribute-value-list* `}` &#124; `?` (The braces are literal; they are returned by the driver.)<br>
 *lista de valores de atributo* :: = *cadeia de caracteres* [`:`*cadeia de caracteres localizada*] &#124; *cadeia de caracteres* [`:` *cadeia de caracteres localizada*] `,` *lista de valores de atributo*<br>
  
 onde *cadeia de caracteres* e *cadeia de caracteres localizada* ter zero ou mais caracteres; *identificador* e *identificador localizado* tem um ou mais caracteres; *palavra-chave de atributo* não diferencia maiusculas de minúsculas; e *atributo-valor* pode diferenciar maiusculas de minúsculas. Devido à conexão cadeia de caracteres de inicialização gramática, palavras-chave, localizados identificadores de arquivo e valores de atributo que contém os caracteres **[]{}(),? \*=! @** devem ser evitadas. Devido a gramática nas informações do sistema, os nomes de fontes de dados e palavras-chave não podem conter uma barra invertida (\\) caracteres.  
  
 A sintaxe de cadeia de conexão de resultado de procura é usada de acordo com as regras semânticas a seguir:  
  
-   Se um asterisco (\*) precede um *palavra-chave de atributo*, o *atributo* é opcional e pode ser omitido na próxima chamada para **SQLBrowseConnect**.  
  
-   As palavras-chave do atributo **UID** e **PWD** têm o mesmo significado conforme definido em **SQLDriverConnect**.  
  
-   Um *-definido-atributo-palavra-chave driver* nomes do tipo de atributo para o qual um valor de atributo pode ser fornecido. Por exemplo, talvez seja **servidor**, **banco de dados**, **HOST**, ou **DBMS**.  
  
-   *ODBC-atributo-palavras-chave* e *-definido-atributo-palavras-chave driver* incluem uma versão localizada ou amigável da palavra-chave. Isso pode ser usado por aplicativos como um rótulo na caixa de diálogo. No entanto, **UID**, **PWD**, ou o *identificador* sozinho, deve ser usado ao passar uma cadeia de caracteres de solicitação de navegação para o driver.  
  
-   O {*lista de valores de atributo*} é uma enumeração dos valores reais válido para o correspondente *palavra-chave de atributo*. Observe que as chaves ({}) não indicam uma lista de opções; elas são retornadas pelo driver. Por exemplo, ele pode ser uma lista de nomes de servidor ou uma lista de nomes de banco de dados.  
  
-   Se o *atributo-valor* é um ponto único de interrogação (?), um único valor corresponde do *palavra-chave de atributo*. Por exemplo, UID = JohnS; PWD = Sesame.  
  
-   Cada chamada para **SQLBrowseConnect** retorna apenas as informações necessárias para atender o próximo nível do processo de conexão. O driver associa informações de estado com o identificador de conexão para que o contexto sempre pode ser determinado em cada chamada.  
  
## <a name="using-sqlbrowseconnect"></a>Usando SQLBrowseConnect  
 **SQLBrowseConnect** requer uma conexão alocado. O Gerenciador de Driver carrega o driver que foi especificado ou que corresponde ao nome de fonte de dados especificado na cadeia de conexão de solicitação de navegação inicial; Para obter informações sobre quando isso ocorre, consulte a seção "Comentários" [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). O driver pode estabelecer uma conexão com a fonte de dados durante o processo de localização. Se **SQLBrowseConnect** retornará SQL_ERROR, pendente, as conexões são encerradas e a conexão é retornado para um estado desconectado.  
  
> [!NOTE]  
>  **SQLBrowseConnect** não dá suporte a pool de conexão. Se **SQLBrowseConnect** é chamado enquanto o pooling de conexão é habilitada, SQLSTATE HY000 (erro geral) será retornado.  
  
 Quando **SQLBrowseConnect** é chamado pela primeira vez em uma conexão, a cadeia de caracteres de conexão do Procurar solicitação deve conter o **DSN** palavra-chave ou o **DRIVER** palavra-chave. Se a cadeia de caracteres de conexão do Procurar solicitação contém o **DSN** palavra-chave, o Gerenciador de Driver localiza uma especificação de fonte de dados correspondente nas informações do sistema:  
  
-   Se o Gerenciador de Driver localiza a especificação de fonte de dados correspondente, ele carrega o driver associado DLL; o driver pode recuperar informações sobre a fonte de dados das informações do sistema.  
  
-   Se o Gerenciador de Driver não é possível localizar a especificação de fonte de dados correspondente, ele localiza a especificação de fonte de dados padrão e carrega o driver associado DLL; o driver pode recuperar informações sobre a fonte de dados padrão das informações do sistema. "DEFAULT" é passada para o driver para o DSN.  
  
-   Se o Gerenciador de Driver não é possível localizar a especificação de fonte de dados correspondente e não há nenhuma especificação de fonte de dados padrão, ele retornará SQL_ERROR com SQLSTATE IM002 (fonte de dados não encontrado e nenhum driver padrão especificado).  
  
 Se a cadeia de caracteres de conexão do Procurar solicitação contém o **DRIVER** palavra-chave, o Gerenciador de Driver carrega o driver especificado; ele não tenta localizar uma fonte de dados nas informações do sistema. Porque o **DRIVER** palavra-chave não usar as informações das informações do sistema, o driver deve definir palavras-chave suficientes para que um driver pode se conectar a uma fonte de dados usando apenas as informações nas cadeias de conexão de solicitação de navegação.  
  
 Em cada chamada para **SQLBrowseConnect**, o aplicativo especifica os valores de atributo de conexão na cadeia de conexão de solicitação de navegação. O driver retorna níveis sucessivos de atributos e valores de atributo na cadeia de conexão do resultado de procurar; ele retorna SQL_NEED_DATA como atributos de conexão que ainda não foram enumerados na cadeia de conexão de solicitação de navegação. O aplicativo usa o conteúdo da cadeia de caracteres de conexão de resultado Procurar para construir a cadeia de caracteres de conexão de solicitação de navegação para a próxima chamada para **SQLBrowseConnect**. Todos os atributos obrigatórios (aqueles não precedido por um asterisco no *OutConnectionString* argumento) devem ser incluídos na próxima chamada para **SQLBrowseConnect**. Observe que o aplicativo não pode usar o conteúdo de cadeias de conexão de resultado de procurar anterior ao criar a cadeia de conexão de solicitação procurar atual; ou seja, ele não é possível especificar valores diferentes para os atributos definidos nos níveis anteriores.  
  
 Quando todos os níveis de conexão e seus atributos associados foram enumerados, o driver retornará SQL_SUCCESS, a conexão à fonte de dados for concluída e uma cadeia de caracteres de conexão completa é retornada ao aplicativo. A cadeia de caracteres de conexão é adequada a ser usado em conjunto com **SQLDriverConnect**, com a opção SQL_DRIVER_NOPROMPT para estabelecer a conexão de outro. A cadeia de caracteres de conexão completa não pode ser usada em outra chamada para **SQLBrowseConnect**, no entanto; se **SQLBrowseConnect** foi chamado novamente, toda a sequência de chamadas teria que ser repetido.  
  
 **SQLBrowseConnect** também retornará SQL_NEED_DATA se houver erros não fatais, recuperáveis durante o processo de procurar; por exemplo, uma senha inválida ou palavra-chave de atributo fornecida pelo aplicativo. Quando SQL_NEED_DATA é retornado e a cadeia de caracteres de conexão de resultado de procura é alterada, ocorreu um erro e o aplicativo pode chamar **SQLGetDiagRec** para retornar o SQLSTATE para erros de tempo de navegação. Isso permite que o aplicativo para corrigir o atributo e continuar o procurar.  
  
 Um aplicativo pode encerrar o processo de procurar a qualquer momento chamando **SQLDisconnect**. O driver irá encerrar quaisquer conexões pendentes e retornar a conexão para um estado desconectado.  
  
 Se operações assíncronas estão habilitada no identificador da conexão, **SQLBrowseConnect** também podem retornar SQL_STILL_EXECUTING. Quando ele retorna SQL_NEED_DATA, um aplicativo deve usar **SQLDisconnect** para cancelar o processo de procurar. Se **SQLBrowseConnect** retornará SQL_STILL_EXECUTING, um aplicativo deve usar **SQLCancelHandle** para cancelar a operação em andamento. Chamando **SQLCancelHandle** depois que a função retorna SQL_NEED_DATA não tem nenhum efeito.  
  
 Para obter mais informações, consulte [conectando com SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Se um driver compatível com **SQLBrowseConnect**, a seção de palavra-chave driver nas informações do sistema para o driver deve conter o **ConnectFunctions** palavra-chave com o terceiro caractere definido como "Y".  
  
## <a name="code-example"></a>Exemplo de código  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar `Trusted_Connection=yes` em vez das informações de ID e a senha do usuário na cadeia de conexão.  
  
 No exemplo a seguir, um aplicativo chama **SQLBrowseConnect** repetidamente. Cada vez que **SQLBrowseConnect** retorna SQL_NEED_DATA, ele passa informações sobre os dados necessários no \* *OutConnectionString*. A aplicativo passa *OutConnectionString* para sua rotina de **GetUserInput** (não mostrado). **GetUserInput** analisa as informações, cria e exibe uma caixa de diálogo e retorna as informações inseridas pelo usuário em \* *InConnectionString*. O aplicativo passa as informações do usuário para o driver na próxima chamada para **SQLBrowseConnect**. Depois que o aplicativo tiver fornecido todas as informações necessárias para se conectar à fonte de dados, o driver **SQLBrowseConnect** retorna SQL_SUCCESS e o aplicativo continua.  
  
 Para obter um exemplo mais detalhado de se conectar a um driver do SQL Server chamando **SQLBrowseConnect**, consulte [exemplo de navegação do SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md).  
  
 Por exemplo, para se conectar aos dados de vendas de origem, as seguintes ações podem ocorrer. Primeiro, o aplicativo passa a seguinte cadeia de caracteres para **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 O Gerenciador de Driver carrega o driver associado com a fonte de dados de vendas. Depois, ele chama o driver **SQLBrowseConnect** função com os mesmos argumentos que ele recebeu do aplicativo. O driver retorna a seguinte cadeia de caracteres em **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 O aplicativo passa essa cadeia de caracteres para seus **GetUserInput** rotina, que cria uma caixa de diálogo que solicita ao usuário para selecionar o servidor de verde, vermelho ou azul e insira uma ID de usuário e senha. A rotina passa as seguintes informações especificadas pelo usuário novamente \* *InConnectionString*, que o aplicativo passa para **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** usa essas informações para se conectar ao servidor vermelho como Smith com a senha Sesame e, em seguida, retorna a seguinte cadeia de caracteres em **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 O aplicativo passa essa cadeia de caracteres para seus **GetUserInput** rotina, que cria uma caixa de diálogo que solicita ao usuário selecionar um banco de dados. O usuário seleciona empdata e o aplicativo chama **SQLBrowseConnect** uma última vez com essa cadeia de caracteres:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Essa é a parte final das informações que o driver precisa se conectar à fonte de dados; **SQLBrowseConnect** retorna SQL_SUCCESS, e **OutConnectionString* contém a cadeia de caracteres de conexão concluído:  
  
```  
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
|Conectando a uma fonte de dados usando uma caixa de diálogo ou cadeia de caracteres de conexão|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando atributos e descrições de driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberando um identificador de conexão|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
