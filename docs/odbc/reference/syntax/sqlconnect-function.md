---
title: Função SQLConnect | Microsoft Docs
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
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c125516f2cc46c1391f74e016b3d4e9487c8dc57
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922741"
---
# <a name="sqlconnect-function"></a>Função SQLConnect
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLConnect** estabelece conexões com um driver e uma fonte de dados. O identificador de conexão faz referência a armazenamento de todas as informações sobre a conexão à fonte de dados, incluindo status, o estado de transação e informações de erro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador da conexão*  
 [Entrada] Identificador de Conexão.  
  
 *ServerName*  
 [Entrada] Nome da fonte de dados. Os dados podem ser localizados no mesmo computador que o programa, ou em outro computador em algum lugar em uma rede. Para obter informações sobre como um aplicativo escolhe uma fonte de dados, consulte [escolhendo uma fonte de dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Entrada] Comprimento de **ServerName* em caracteres.  
  
 *UserName*  
 [Entrada] Identificador de usuário.  
  
 *NameLength2*  
 [Entrada] Comprimento de **nome de usuário* em caracteres.  
  
 *Autenticação*  
 [Entrada] Cadeia de caracteres de autenticação (normalmente a senha).  
  
 *NameLength3*  
 [Entrada] Comprimento de **autenticação* em caracteres.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLConnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DBC e um *tratar* de *identificador da conexão*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLConnect** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O driver não oferecia suporte para o valor especificado do *ValuePtr* argumento **SQLSetConnectAttr** e substituído, um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08001|Não é possível estabelecer a conexão do cliente|O driver não pôde estabelecer uma conexão com a fonte de dados.|  
|08002|Nome da Conexão em uso|(DM) especificado *identificador da conexão* já tenha sido usada para estabelecer uma conexão com uma fonte de dados e a conexão foram aberta ou o usuário foi navegando para uma conexão.|  
|08004|O servidor recusou a conexão|A fonte de dados rejeitados o estabelecimento da conexão por motivos de implementação definida.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver estava tentando conectar-se antes do processamento da função foi concluída.|  
|28000|Especificação de autorização inválida|O valor especificado para o argumento *UserName* ou o valor especificado para o argumento *autenticação* violou as restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O Gerenciador de Driver (DM) não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *identificador da conexão*. O **SQLConnect** função foi chamada e antes ele concluiu a execução, [SQLCancelHandle função](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado no *identificador da conexão*e, em seguida, o **SQLConnect** função foi chamada novamente no *identificador da conexão*.<br /><br /> Ou, o **SQLConnect** função foi chamada e antes ele concluiu a execução, **SQLCancelHandle** foi chamado no *identificador da conexão* de um thread diferente em uma aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona (não la) foi chamada para o *identificador da conexão* e ainda estava em execução quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *NameLength1*, *NameLength2*, ou *NameLength3* era menor que 0 mas não igual a SQL_NTS.<br /><br /> (DM) o valor especificado para o argumento *NameLength1* excedeu o comprimento máximo para um nome de fonte de dados.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da conexão à fonte de dados foi concluída. O período de tempo limite é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|Driver não oferece suporte à execução de função assíncrona de nível de conexão|(DM) o aplicativo ativado a operação assíncrona no identificador da conexão antes de fazer a conexão. No entanto, o driver não oferece suporte a operações assíncronas no identificador da conexão.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver especificado pelo nome de fonte de dados não dá suporte para a função.|  
|IM002|Fonte de dados não encontrado e nenhum driver padrão especificado|(DM) a fonte de dados especificado no argumento de nome *ServerName* não foi encontrado nas informações do sistema, nem houve uma especificação de driver padrão.|  
|IM003|O driver especificado não pode ser conectado a|O driver de (DM) listados nos dados de especificação de origem em informações do sistema não foi encontrada ou não pôde ser conectada por algum outro motivo.|  
|IM004|Falha de SQLAllocHandle do driver em SQL_HANDLE_ENV|(DM) durante **SQLConnect**, o Gerenciador de Driver chamado o driver **SQLAllocHandle** funcionar com um *HandleType* SQL_HANDLE_ENV e o driver retornou um erro.|  
|IM005|Falha de SQLAllocHandle do driver em SQL_HANDLE_DBC|(DM) durante **SQLConnect**, o Gerenciador de Driver chamado o driver **SQLAllocHandle** funcionar com um *HandleType* SQL_HANDLE_DBC e o driver retornou um erro.|  
|IM006|Falha de SQLSetConnectAttr do driver|Durante a **SQLConnect**, o Gerenciador de Driver chamado o driver **SQLSetConnectAttr** função e o driver retornaram um erro. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|IM009|Não é possível conectar-se a DLL de conversão|O driver não pôde se conectar à conversão de DLL que foi especificado para a fonte de dados.|  
|IM010|Nome de fonte de dados muito longo|(DM)  *\*ServerName* tinha mais de SQL_MAX_DSN_LENGTH caracteres.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o Driver e o aplicativo|Aplicativo de 32 bits (DM) usa um DSN que se conectar a um driver de 64 bits. ou vice-versa.|  
|IM015|Falha SQLConnect do driver em SQL_HANDLE_DBC_INFO_HANDLE|Se um driver retornará SQL_ERROR, o Gerenciador de Driver retornará SQL_ERROR para o aplicativo e a conexão falhará.<br /><br /> Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
|S1118|Driver não dá suporte a notificação assíncrona|Quando o driver não dá suporte a notificação assíncrona, você não pode definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre por que um aplicativo usa **SQLConnect**, consulte [conectar-se com o SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 O Gerenciador de Driver não se conecta a um driver até que o aplicativo chama uma função (**SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**) para conectar-se para o driver. Até esse ponto, o Gerenciador de Driver funciona com seus próprio identificadores e gerencia informações de conexão. Quando o aplicativo chama uma função de conexão, o Gerenciador de Driver verifica se um driver está conectado atualmente à especificado *identificador da conexão*:  
  
-   Se um driver não está conectado a, o Gerenciador de Driver conecta-se para o driver e chamadas **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV, **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC, **SQLSetConnectAttr** (se o aplicativo especificado quaisquer atributos de conexão) e a função de conexão no driver. O Gerenciador de Driver retornará SQLSTATE IM006 (do Driver **SQLSetConnectOption** falha) e SQL_SUCCESS_WITH_INFO para a função de conexão se o driver retornou um erro de **SQLSetConnectAttr**. Para obter mais informações, consulte [se conectar a uma fonte de dados ou Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md).  
  
-   Se o driver especificado já está conectado no *identificador da conexão*, o Gerenciador de Driver chama a função de conexão no driver. Nesse caso, o driver deve garantir que a conexão de todos os atributos para o *identificador da conexão* manter suas configurações atuais.  
  
-   Se um driver diferente está conectado à, chama o Gerenciador de Driver **SQLFreeHandle** com um *HandleType* SQL_HANDLE_DBC, e, em seguida, se nenhum outro driver está conectado no ambiente, chama **SQLFreeHandle** com um *HandleType* SQL_HANDLE_ENV no driver conectado e, em seguida, desconecta o driver. Ele executa as mesmas operações como quando um driver não está conectado ao.  
  
 Em seguida, o driver aloca identificadores e inicializa a próprio.  
  
 Quando o aplicativo chama **SQLDisconnect**, as chamadas de Gerenciador de Driver **SQLDisconnect** no driver. No entanto, não desconecte o driver. Isso impede que o driver na memória para aplicativos que repetidamente conectar e desconectar de uma fonte de dados. Quando o aplicativo chama **SQLFreeHandle** com um *HandleType* SQL_HANDLE_DBC, chama o Gerenciador de Driver **SQLFreeHandle** com um *HandleType*  SQL_HANDLE_DBC e **SQLFreeHandle** com um *HandleType* SQL_HANDLE_ENV no driver e, em seguida, desconecta o driver.  
  
 Um aplicativo ODBC pode estabelecer uma conexão de mais de um.  
  
## <a name="driver-manager-guidelines"></a>Diretrizes de Gerenciador de driver  
 O conteúdo de **ServerName* afetam como o Gerenciador de Driver e um driver funcionam juntos para estabelecer uma conexão com uma fonte de dados.  
  
-   Se \* *ServerName* contém um nome de fonte de dados válido, o Gerenciador de Driver localiza a especificação de fonte de dados correspondente nas informações do sistema e conecta-se para o driver associado. O Gerenciador de Driver passa cada **SQLConnect** argumento para o driver.  
  
-   Se o nome da fonte de dados não pode ser encontrado ou *ServerName* é um ponteiro nulo, o Gerenciador de Driver localiza a especificação de fonte de dados padrão e se conecta ao driver associado. O Gerenciador de Driver passa para o driver de *UserName* e *autenticação* argumentos sem modificações e "Padrão" para o *ServerName* argumento.  
  
-   Se o *ServerName* argumento é "Padrão", o Gerenciador de Driver localiza a especificação de fonte de dados padrão e se conecta ao driver associado. O Gerenciador de Driver passa cada **SQLConnect** argumento para o driver.  
  
-   Se o nome da fonte de dados não pode ser encontrado ou *ServerName* é um ponteiro nulo e o padrão de especificação de fonte de dados não existir, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE IM002 (fonte de dados nome não foi encontrado e nenhum padrão driver especificado).  
  
 Depois que ele está conectado a pelo Gerenciador de Driver, um driver pode localizar sua especificação de fonte de dados correspondente nas informações do sistema e usar informações específicas do driver da especificação para concluir seu conjunto de informações de conexão necessárias.  
  
 Se uma biblioteca de conversão padrão é especificada nas informações do sistema para a fonte de dados, o driver se conecta a ele. Uma biblioteca de conversão diferentes pode ser conectada a chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_LIB. Uma opção de conversão pode ser especificada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Se um driver compatível com **SQLConnect**, a seção de palavra-chave driver as informações do sistema para o driver deve conter o **ConnectFunctions** palavra-chave com o primeiro caractere é definido como "Y".  
  
### <a name="connection-pooling"></a>Pool de conexões  
 Pooling de Conexão permite que um aplicativo reutilizar uma conexão que já foi criado. Quando o pooling de conexão é habilitado e **SQLConnect** é chamado, o Gerenciador de Driver tenta fazer a conexão usando uma conexão que é parte de um pool de conexões em um ambiente que foram designados para o pool de conexão. Esse ambiente é um ambiente compartilhado que é usado por todos os aplicativos que usam as conexões no pool.  
  
 Pooling de Conexão está habilitada antes do ambiente é alocado chamando **SQLSetEnvAttr** definir SQL_ATTR_CONNECTION_POOLING para SQL_CP_ONE_PER_DRIVER (que especifica um máximo de um pool por driver) ou SQL_CP_ONE_PER_HENV (que especifica um máximo de um pool por ambiente). **SQLSetEnvAttr** nesse caso é chamado com *EnvironmentHandle* definido como null, o que torna o atributo de um atributo de nível de processo. Se SQL_ATTR_CONNECTION_POOLING for definido como SQL_CP_OFF, o pooling de conexão está desabilitada.  
  
 Após a habilitação do pool de conexão, **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV é chamado para alocar um ambiente. O ambiente alocado por essa chamada é um ambiente compartilhado porque o pool de conexão foi ativado. No entanto, o ambiente que será usado não é determinado até **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC é chamado.  
  
 **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC é chamado para alocar uma conexão. O Gerenciador de Driver tenta encontrar um ambiente compartilhado existente que correspondem aos atributos de ambiente definidos pelo aplicativo. Se tal ambiente não existir, um será criado como um implícito *ambiente compartilhado*. Se um ambiente compartilhado correspondente for encontrado, o identificador de ambiente é retornado para o aplicativo e sua contagem de referência é incrementada.  
  
 No entanto, a conexão será usado não é determinada até **SQLConnect** é chamado. Nesse ponto, o Gerenciador de Driver tenta localizar uma conexão existente no pool de conexão que corresponde aos critérios solicitados pelo aplicativo. Esses critérios incluem as opções de conexão solicitadas na chamada para **SQLConnect** (os valores de *ServerName*, *UserName*, e  *Autenticação* palavras-chave) e defina os atributos de conexão desde **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC foi chamado. O Gerenciador de Driver verifica esses critérios em relação às palavras-chave de conexão correspondente e atributos em conexões no pool. Se uma correspondência for encontrada, a conexão do pool é usada. Se nenhuma correspondência for encontrada, é criada uma nova conexão.  
  
 Se o atributo de ambiente SQL_ATTR_CP_MATCH é definido como SQL_CP_STRICT_MATCH, a correspondência deve ser exata para uma conexão em pool a ser usado. Se o atributo de ambiente SQL_ATTR_CP_MATCH é definido como SQL_CP_RELAXED_MATCH, a conexão opções na chamada para **SQLConnect** devem coincidir, mas não todos os atributos de conexão devem corresponder.  
  
 As seguintes regras são aplicadas quando um atributo de conexão, conforme definido pelo aplicativo antes de **SQLConnect** é chamado, não coincide com o atributo de conexão da conexão do pool:  
  
-   Se o atributo de conexão deve ser definido antes que a conexão é feita:  
  
     Se SQL_ATTR_CP_MATCH for SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE na conexão em pool deve ser idêntico ao atributo definido pelo aplicativo. Se SQL_CP_RELAXED_MATCH, os valores de SQL_ATTR_PACKET_SIZE pode ser diferente.  
  
     O valor de SQL_ATTR_LOGIN_VALUE não afeta a correspondência.  
  
-   Se o atributo de conexão pode ser definido antes ou depois que a conexão é estabelecida:  
  
     Se o atributo de conexão não foi definido pelo aplicativo, mas foi definido na conexão no pool, e não há um padrão, o atributo de conexão em que a conexão em pool é redefinido para o padrão e uma correspondência é declarada. Se não houver nenhum padrão, a conexão em pool não é considerado uma correspondência.  
  
     Se o atributo de conexão foi definido pelo aplicativo, mas não foi definido na conexão no pool, o atributo de conexão no pool é alterado ao conjunto pelo aplicativo e uma correspondência é declarada.  
  
     Se o atributo de conexão foi definido pelo aplicativo e também tiver sido definido na conexão no pool, mas os valores forem diferentes, o valor do atributo de conexão do aplicativo é usado e uma correspondência é declarada.  
  
-   Se os valores dos atributos de conexão específicos do driver não são idênticos e SQL_ATTR_CP_MATCH é definido como SQL_CP_STRICT_MATCH, a conexão no pool não será usado.  
  
 Quando o aplicativo chama **SQLDisconnect** para desconectar, a conexão é retornado para o pool de conexão e está disponível para reutilização.  
  
### <a name="optimizing-connection-pooling-performance"></a>Otimizando o desempenho do pool de Conexão  
 Quando as transações distribuídas estão envolvidas, é possível otimizar o desempenho usando o pool de conexão **SQL_DTC_TRANSITION_COST**, que é um bitmask SQLUINTEGER. As transições chamadas são as transições do atributo de conexão SQL_ATTR_ENLIST_IN_DTC indo de valor 0 como diferente de zero e vice-versa. Isso é uma conexão de não inscrita em uma transação distribuída inscrita em uma transação distribuída e vice-versa. Dependendo de como o driver implementou inscrição (definir atributo de conexão SQL_ATTR_ENLIST_IN_DTC), essas transições podem ser caras e, portanto, devem ser evitadas para melhor desempenho.  
  
 O valor retornado pelo driver contém qualquer combinação destes bits:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, quando definido, implica que o zero a transição diferente de zero é significativamente mais caro do que uma transição de zero para outro valor diferente de zero (inscrição de uma conexão anteriormente inscrito na sua próxima transação).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, quando definido, implica diferente de zero para zero transição é significativamente mais caro do que usando uma conexão cujo atributo SQL_ATTR_ENLIST_IN_DTC já está definido como zero.  
  
 Há um desempenho em relação ao equilíbrio de uso de conexão. Se um driver indica que uma ou mais dessas transições são caras, pooler de conexão do Gerenciador de driver responde a isso, mantendo mais conexões no pool. Algumas conexões no pool são preferenciais para uso não transacional, e alguns são preferenciais para uso transacional. No entanto, se o driver indica que essas transições não são caras, menos conexões podem ser usadas, talvez alternando entre não transacionais e de uso transacional.  
  
 Drivers que não oferecem suporte a SQL_ATTR_ENLIST_IN_DTC não é necessário dar suporte a SQL_DTC_TRANSITION_COST. Drivers que oferecem suporte a SQL_ATTR_ENLIST_IN_DTC mas não SQL_DTC_TRANSITION_COST, supõe-se que as transições não são caras, como se o driver retornou 0 (nenhum conjunto de bits) para esse valor.  
  
 Embora SQL_DTC_TRANSITION_COST foi introduzido no ODBC 3.5, um ODBC 2. *x* driver também der suporte a isso porque o Gerenciador de driver irá consultar essas informações, independentemente da versão do driver.  
  
### <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo aloca ambiente e conexão identificadores. Em seguida, ele se conecta à fonte de dados SalesOrders com o ID JohnS de usuário e a senha Sesame e processa dados. Quando tiver concluído o processamento de dados, ele se desconecta da fonte de dados e libera os identificadores.  
  
```  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
### <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Descobrir e enumerar os valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Desconectando de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conectando a uma fonte de dados usando uma caixa de diálogo ou cadeia de caracteres de conexão|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
