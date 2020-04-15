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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301336"
---
# <a name="sqlbrowseconnect-function"></a>Função SQLBrowseConnect
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **O SQLBrowseConnect** suporta um método iterativo de descobrir e enumerar os atributos e valores de atributos necessários para se conectar a uma fonte de dados. Cada chamada para **SQLBrowseConnect** retorna níveis sucessivos de atributos e valores de atributos. Quando todos os níveis foram enumerados, uma conexão com a fonte de dados é concluída e uma seqüência completa de conexão é retornada pelo **SQLBrowseConnect**. Um código de retorno de SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO indica que todas as informações de conexão foram especificadas e o aplicativo agora está conectado à fonte de dados.  
  
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
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *String de inconexão*  
 [Entrada] Procurar seqüência de conexão de solicitação (consulte "*InConnectionString* Argument" em "Comentários").  
  
 *Comprimento da corda1*  
 [Entrada] Comprimento de **InConnectionString* em caracteres.  
  
 *OutConnectionString*  
 [Saída] Ponteiro para um buffer de caracteres no qual retornar a seqüência de conexão de resultado de navegação (consulte *" OutConnectionString* Argument" em "Comentários").  
  
 Se *OutConnectionString* for NULL, *StringLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado por *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Comprimento, em caracteres, do buffer ** OutConnectionString.*  
  
 *StringLength2Ptr*  
 [Saída] O número total de caracteres (excluindo o \*término nulo) disponível para retornar em *OutConnectionString*. Se o número de caracteres disponíveis para retornar for maior \*ou igual a *BufferLength,* a seqüência de conexão em *OutConnectionString* será truncada em *BufferLength* menos o comprimento de um caractere de rescisão nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLBrowseConnect** retorna SQL_ERROR, SQL_SUCCESS_WITH_INFO ou SQL_NEED_DATA, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça de ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLBrowseConnect** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \*buffer *OutConnectionString* não era grande o suficiente para retornar toda a seqüência de conexão de resultado da navegação, de modo que a seqüência foi truncada. O buffer **StringLength2Ptr* contém o comprimento da seqüência de conexão de resultado de navegação não truncada. (Função retorna SQL_NEED_DATA.)|  
|01S00|Atributo de seqüência de conexão inválido|Uma palavra-chave de atributo inválida foi especificada na seqüência de conexão de solicitação de navegação *(InConnectionString*). (Função retorna SQL_NEED_DATA.)<br /><br /> Uma palavra-chave de atributo foi especificada na seqüência de conexão de solicitação de navegação *(InConnectionString)* que não se aplica ao nível de conexão atual. (Função retorna SQL_NEED_DATA.)|  
|01S02|Valor alterado|O driver não suportava o valor especificado do argumento *ValuePtr* no **SQLSetConnectAttr** e substituiu um valor semelhante. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de estabelecer conexão|O motorista não conseguiu estabelecer uma conexão com a fonte de dados.|  
|08002|Nome de conexão em uso|(DM) A conexão especificada já havia sido usada para estabelecer uma conexão com uma fonte de dados, e a conexão estava aberta.|  
|08004|Servidor rejeitou a conexão|A fonte de dados rejeitou o estabelecimento da conexão por razões definidas pela implementação.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o motorista estava tentando se conectar falhou antes que a função concluísse o processamento.|  
|28000|Especificação de autorização inválida|O identificador do usuário ou a seqüência de autorização ou ambos, conforme especificado na seqüência de conexão de solicitação de navegação *(InConnectionString),* violaram as restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) O Driver Manager não conseguiu alocar a memória necessária para suportar a execução ou o cumprimento da função.<br /><br /> O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|Uma operação assíncrona foi cancelada chamando [sqlcancelhandle function](../../../odbc/reference/syntax/sqlcancelhandle-function.md). Em seguida, a função original foi chamada novamente no *ConnectionHandle*.<br /><br /> Uma operação foi cancelada chamando **SQLCancelHandle** no *ConnectionHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava sendo executada quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para o argumento *StringLength1* era inferior a 0 e não era igual a SQL_NTS.<br /><br /> (DM) O valor especificado para *o argumento BufferLength* foi inferior a 0.|  
|HY114|Driver não suporta execução de função assíncrona nível de conexão|(DM) O aplicativo habilitou a operação assíncrona no cabo de conexão antes de fazer a conexão. No entanto, o driver não suporta operação assíncrona no cabo de conexão.|  
|HYT00|Tempo limite esgotado|O período de tempo de tempo de login expirou antes da conexão com a fonte de dados concluída. O período de tempo é definido através de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver correspondente ao nome de origem de dados especificado não suporta a função.|  
|IM002|Fonte de dados não encontrada e nenhum driver padrão especificado|(DM) O nome de origem dos dados especificado na seqüência de conexão de solicitação de navegação *(InConnectionString)* não foi encontrado nas informações do sistema, nem havia uma especificação padrão do driver.<br /><br /> (DM) A fonte de dados ODBC e as informações padrão do driver não puderam ser encontradas nas informações do sistema.|  
|IM003|Driver especificado não pôde ser carregado|(DM) O driver listado na especificação de origem de dados nas informações do sistema ou especificado pela palavra-chave **DRIVER** não foi encontrado ou não pôde ser carregado por algum outro motivo.|  
|IM004|**SQLAllocHandle** do motorista em SQL_HANDLE _ENV falhou|(DM) Durante o **SQLBrowseConnect,** o Driver Manager ligou para a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_ENV e o motorista retornou um erro.|  
|IM005|**SQLAllocHandle** do driver em SQL_HANDLE_DBC falhou|(DM) Durante o **SQLBrowseConnect,** o Driver Manager ligou para a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_DBC e o motorista retornou um erro.|  
|IM006|Falha no **SQLSetConnectAttr** do driver|(DM) Durante o **SQLBrowseConnect,** o Driver Manager ligou para a função **SQLSetConnectAttr** do driver e o driver retornou um erro.|  
|IM009|Não é possível carregar dll de tradução|O driver não conseguiu carregar a DLL de tradução especificada para a fonte de dados ou para a conexão.|  
|IM010|Nome de origem de dados muito longo|(DM) O valor de atributo para a palavra-chave DSN foi maior do que SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nome do motorista muito longo|(DM) O valor de atributo para a palavra-chave DRIVER era superior a 255 caracteres.|  
|IM012|Erro de sintaxe de palavra-chave DRIVER|(DM) O par de valor de palavra-chave para a palavra-chave DRIVER continha um erro de sintaxe.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o Driver e o Aplicativo|(DM) O aplicativo de 32 bits usa uma conexão DSN a um driver de 64 bits; ou vice-versa.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
|S1118|O driver não suporta notificação assíncrona|Quando o driver não suporta notificação assíncrona, não é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>Argumento de string de inconexão  
 Uma seqüência de conexão de solicitação de navegação tem a seguinte sintaxe:  
  
 *string de conexão::=* *atributo*[`;`] &#124; *atributo* `;` *string de conexão;*<br>
 *atribuição* ::= *atributo-palavra-chave*`=`*atributo-valor* `DRIVER=`&#124;`{`[ ] valor de*atributo*[`}`]<br>
 *palavra-chave de atributo* `DSN` ::= &#124; `UID` &#124; `PWD` &#124; *palavra-chave de atributo definido pelo driver*<br>
 *valor do atributo* ::= *caractere-string*<br>
 *palavra-chave de atributo definido pelo driver* ::= *identificador*<br>
  
 onde *a seqüência de caracteres* tem zero ou mais caracteres; *identificador* tem um ou mais caracteres; *apalavra-chave de atributo* não é sensível a maiúsculas e minúsculas; *o valor do atributo* pode ser sensível a maiúsculas e minúsculas; e o valor da palavra-chave **DSN** não consiste apenas em espaços em branco. Por causa da gramática do arquivo de seqüência de conexão e inicialização, palavras-chave e valores de atributos que contêm os caracteres **[];?{} \*=!@** deve ser evitado. Devido à gramática nas informações do sistema, palavras-chave e\\nomes de fonte de dados não podem conter o caractere barra invertida ( ). Para um ODBC 2. *x* driver, chaves são necessárias em torno do valor de atributo para a palavra-chave DRIVER.  
  
 Se alguma palavra-chave for repetida na seqüência de conexão de solicitação de navegação, o driver usará o valor associado à primeira ocorrência da palavra-chave. Se as palavras-chave **DSN** e **DRIVER** estiverem incluídas na mesma seqüência de conexão de solicitação de navegação, o Driver Manager e o driver usam qual palavra-chave aparecer primeiro.  
  
 Para obter informações sobre como um aplicativo escolhe uma fonte de dados ou driver, consulte [Escolher uma Fonte de Dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>Argumento outConnectionString  
 A seqüência de conexão de resultado da navegação é uma lista de atributos de conexão. Um atributo de conexão consiste em uma palavra-chave de atributo e um valor de atributo correspondente. A seqüência de conexão de resultado da navegação tem a seguinte sintaxe:  
  
 *string de conexão::=* *atributo*[`;`] &#124; *atributo* `;` *string de conexão*<br>
 *atributo* `*`::= [ ]*atributo-palavra-chave*`=`*valor-atributo*<br>
 *palavra-chave de atributo* ::= *ODBC-attribute-keyword* &#124; *driver-defined-attribute-attribute-keyword*<br>
 *ODBC-attribute-keyword* =`UID` `PWD`{`:`&#124; `}` `?` `:` `{` *}[localizado-identificador]* *driver-defined-attribute-keyword* ::= *identifier**[localized-identifier]* *attribute-value* ::= *attribute-value-list* &#124; (As chaves são literais; elas são devolvidas pelo driver.)<br>
 *atribuição-valor-list* ::= *caractere-string* `:`*[seqüência de caracteres localizada*] `,` &#124; *caractere-string* `:`*[seqüência de caracteres localizados]* *atributo-valor-list*<br>
  
 onde *a seqüência de caracteres* e *a seqüência de caracteres localizados* têm zero ou mais caracteres; *identificador* e *identificador localizado* têm um ou mais caracteres; *apalavra-chave de atributo* não é sensível a maiúsculas e minúsculas; e *o valor do atributo* pode ser sensível a maiúsculas e minúsculas. Por causa da gramática do arquivo de seqüência de conexões e inicialização, palavras-chave, identificadores localizados e valores de atributos que contêm os caracteres **[];?{} \*=!@** deve ser evitado. Devido à gramática nas informações do sistema, palavras-chave e\\nomes de fonte de dados não podem conter o caractere barra invertida ( ).  
  
 A sintaxe de seqüência de seqüência de conexão de resultados da navegação é usada de acordo com as seguintes regras semânticas:  
  
-   Se um\*asterisco ( ) preceder uma *palavra-chave de atributo,* o *atributo* é opcional e pode ser omitido na próxima chamada para **SQLBrowseConnect**.  
  
-   As palavras-chave de atributo **UID** e **PWD** têm o mesmo significado definido no **SQLDriverConnect**.  
  
-   Uma *palavra-chave de atributo definida* pelo driver nomeia o tipo de atributo para o qual um valor de atributo pode ser fornecido. Por exemplo, pode ser **SERVER,** **DATABASE,** **HOST**ou **DBMS.**  
  
-   *Palavras-chave de atributo ODBC* e *palavras-chave de atributo definido susco* incluem uma versão localizada ou fácil de usar da palavra-chave. Isso pode ser usado por aplicativos como um rótulo em uma caixa de diálogo. No entanto, **UID**, **PWD,** ou o *identificador* sozinho deve ser usado ao passar uma seqüência de solicitação de navegação para o driver.  
  
-   A *{ lista de valor de atributo*} é uma enumeração de valores reais válidos para a *palavra-chave de atributo*correspondente . Observe que os{}aparelhos () não indicam uma lista de opções; eles são devolvidos pelo motorista. Por exemplo, pode ser uma lista de nomes de servidores ou uma lista de nomes de banco de dados.  
  
-   Se o *valor do atributo* for um único ponto de interrogação (?), um único valor corresponde à *palavra-chave*de atributo . Por exemplo, UID=Johns; PWD=Sésamo.  
  
-   Cada chamada para **SQLBrowseConnect** retorna apenas as informações necessárias para satisfazer o próximo nível do processo de conexão. O motorista associa informações do estado com o cabo de conexão para que o contexto possa ser sempre determinado em cada chamada.  
  
## <a name="using-sqlbrowseconnect"></a>Usando sqlbrowseconnect  
 **O SQLBrowseConnect** requer uma conexão alocada. O Gerenciador de driver carrega o driver especificado ou que corresponde ao nome de origem dos dados especificado na seqüência inicial de conexão de solicitação de navegação; para obter informações sobre quando isso ocorrer, consulte a seção "Comentários" na [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). O driver pode estabelecer uma conexão com a fonte de dados durante o processo de navegação. Se **o SQLBrowseConnect** retornar SQL_ERROR, as conexões pendentes serão encerradas e a conexão será devolvida a um estado não conectado.  
  
> [!NOTE]  
>  **O SQLBrowseConnect** não suporta pooldeconexões. Se **o SQLBrowseConnect** for chamado enquanto o pool de conexões estiver ativado, o SQLSTATE HY000 (erro geral) será devolvido.  
  
 Quando **o SQLBrowseConnect** é chamado pela primeira vez em uma conexão, a seqüência de conexão de solicitação de navegação deve conter a palavra-chave **DSN** ou a palavra-chave **DRIVER.** Se a seqüência de conexão de solicitação de navegação contiver a palavra-chave **DSN,** o Gerenciador de driver seleção restaria uma especificação de origem de dados correspondente nas informações do sistema:  
  
-   Se o Gerenciador de driver encontrar a especificação de origem de dados correspondente, ele carregará o DLL do driver associado; o motorista pode recuperar informações sobre a fonte de dados a partir das informações do sistema.  
  
-   Se o Gerenciador de driver não conseguir encontrar a especificação correspondente da fonte de dados, ele localizará a especificação de origem de dados padrão e carregará o DLL do driver associado; o driver pode recuperar informações sobre a fonte de dados padrão das informações do sistema. "DEFAULT" é passado para o driver para o DSN.  
  
-   Se o Gerenciador de driver não conseguir encontrar a especificação correspondente da fonte de dados e não houver especificação padrão de origem de dados, ele retornou SQL_ERROR com o SQLSTATE IM002 (fonte de dados não encontrada e nenhum driver padrão especificado).  
  
 Se a seqüência de conexão de solicitação de navegação contiver a palavra-chave **DRIVER,** o Gerenciador de driver carregará o driver especificado; ele não tenta localizar uma fonte de dados nas informações do sistema. Como a palavra-chave **DRIVER** não usa informações das informações do sistema, o driver deve definir palavras-chave suficientes para que um driver possa se conectar a uma fonte de dados usando apenas as informações nas strings de conexão de solicitação de navegação.  
  
 Em cada chamada para **SQLBrowseConnect,** o aplicativo especifica os valores do atributo de conexão na seqüência de conexão de solicitação de navegação. O driver retorna níveis sucessivos de atributos e valores de atributos na seqüência de conexão de resultados da navegação; ele retorna SQL_NEED_DATA desde que haja atributos de conexão que ainda não foram enumerados na seqüência de conexão de solicitação de navegação. O aplicativo usa o conteúdo da seqüência de conexão de resultado de navegação para criar a seqüência de conexão de solicitação de navegação para a próxima chamada ao **SQLBrowseConnect**. Todos os atributos obrigatórios (aqueles não precedidos por um asterisco no argumento *OutConnectionString)* devem ser incluídos na próxima chamada para **SQLBrowseConnect**. Observe que o aplicativo não pode usar o conteúdo das seqüências de conexão de resultados de navegação anteriorao criar a cadeia de conexão de solicitação de navegação atual; ou seja, não pode especificar valores diferentes para atributos definidos em níveis anteriores.  
  
 Quando todos os níveis de conexão e seus atributos associados forem enumerados, o driver retorna SQL_SUCCESS, a conexão com a fonte de dados está completa e uma seqüência de conexão completa é retornada ao aplicativo. A seqüência de conexões é adequada para usar, em conjunto com o **SQLDriverConnect,** com a opção SQL_DRIVER_NOPROMPT de estabelecer outra conexão. No entanto, a seqüência de conexões completa não pode ser usada em outra chamada para **SQLBrowseConnect;** se **o SQLBrowseConnect** fosse chamado novamente, toda a seqüência de chamadas teria que ser repetida.  
  
 **O SQLBrowseConnect** também retorna SQL_NEED_DATA se houver erros recuperáveis e não fatais durante o processo de navegação; por exemplo, uma senha inválida ou palavra-chave de atributo fornecida pelo aplicativo. Quando SQL_NEED_DATA é retornada e a seqüência de conexão de resultado da navegação não é alterada, ocorreu um erro e o aplicativo pode ligar para o **SQLGetDiagRec** para retornar o SQLSTATE para erros de tempo de navegação. Isso permite que o aplicativo corrija o atributo e continue a navegação.  
  
 Um aplicativo pode encerrar o processo de navegação a qualquer momento, ligando para **SQLDisconnect**. O driver encerrará quaisquer conexões pendentes e devolverá a conexão a um estado não conectado.  
  
 Se as operações assíncronas estiverem habilitadas na alça de conexão, o **SQLBrowseConnect** também poderá retornar SQL_STILL_EXECUTING. Quando ele retorna SQL_NEED_DATA, um aplicativo deve usar **o SQLDisconnect** para cancelar o processo de navegação. Se **o SQLBrowseConnect** retornar SQL_STILL_EXECUTING, um aplicativo deve usar **o SQLCancelHandle** para cancelar a operação em andamento. Chamar **SQLCancelHandle** depois que a função retorna SQL_NEED_DATA não tem efeito.  
  
 Para obter mais informações, consulte [Conectando com SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Se um driver suportar **o SQLBrowseConnect,** a seção de palavras-chave do driver nas informações do sistema para o driver deve conter a palavra-chave **ConnectFunctions** com o terceiro caractere definido como "Y".  
  
## <a name="code-example"></a>Exemplo de código  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de origem `Trusted_Connection=yes` de dados que suporta a autenticação do Windows, você deve especificar, em vez de Informações de ID do usuário e senha na seqüência de conexões.  
  
 No exemplo a seguir, um aplicativo chama **SQLBrowseConnect** repetidamente. Cada vez que **o SQLBrowseConnect** retorna SQL_NEED_DATA, ele \*repassa informações sobre os dados necessários no *OutConnectionString*. O aplicativo passa *OutConnectionString* para sua rotina **GetUserInput** (não mostrado). **GetUserInput** analisa as informações, constrói e exibe uma caixa de diálogo e \*retorna as informações inseridas pelo usuário no *InConnectionString*. O aplicativo passa as informações do usuário para o driver na próxima chamada para **SQLBrowseConnect**. Depois que o aplicativo forneceu todas as informações necessárias para que o driver se conecte à fonte de dados, o **SQLBrowseConnect** retorna SQL_SUCCESS e o aplicativo prossegue.  
  
 Para obter um exemplo mais detalhado de conexão a um driver do SQL Server ligando para **o SQLBrowseConnect,** consulte O exemplo de [navegação do servidor SQL](../../../odbc/reference/develop-app/sql-server-browsing-example.md).  
  
 Por exemplo, para conectar-se à fonte de dados Sales, as seguintes ações podem ocorrer. Primeiro, o aplicativo passa a seguinte seqüência para **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 O Driver Manager carrega o driver associado à fonte de dados Sales. Em seguida, ele chama a função **SQLBrowseConnect** do driver com os mesmos argumentos recebidos do aplicativo. O driver retorna a seguinte seqüência em **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 O aplicativo passa essa seqüência para sua rotina **GetUserInput,** que constrói uma caixa de diálogo que pede ao usuário para selecionar o servidor vermelho, azul ou verde e inserir um ID do usuário e senha. A rotina passa as seguintes informações \*especificadas pelo usuário de volta no *InConnectionString*, que o aplicativo passa para **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** usa essas informações para se conectar ao servidor vermelho como Smith com a senha Sesame e, em seguida, retorna a seguinte seqüência em **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 O aplicativo passa essa seqüência para sua rotina **GetUserInput,** que constrói uma caixa de diálogo que pede ao usuário para selecionar um banco de dados. O usuário seleciona empdata e o aplicativo chama **SQLBrowseConect** e uma última vez com esta string:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Esta é a última informação que o motorista precisa para se conectar à fonte de dados; **O SQLBrowseConnect** retorna SQL_SUCCESS e **OutConnectionString* contém a seqüência de conexões concluída:  
  
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
|Alocando uma alça de conexão|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectando-se de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma seqüência de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando descrições e atributos do driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberando uma alça de conexão|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
