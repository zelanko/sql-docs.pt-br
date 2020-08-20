---
description: Função SQLConnect
title: Função SQLConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714bc6f69a72609ee266effff71f1898d62ec7d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461198"
---
# <a name="sqlconnect-function"></a>Função SQLConnect
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 O **SQLConnect** estabelece conexões com um driver e uma fonte de dados. O identificador de conexão faz referência ao armazenamento de todas as informações sobre a conexão com a fonte de dados, incluindo status, estado da transação e informações de erro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *ServerName*  
 Entrada Nome da fonte de dados. Os dados podem estar localizados no mesmo computador que o programa ou em outro computador em algum lugar em uma rede. Para obter informações sobre como um aplicativo escolhe uma fonte de dados, consulte [escolhendo uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 Entrada Comprimento de **ServerName* em caracteres.  
  
 *UserName*  
 Entrada Identificador de usuário.  
  
 *NameLength2*  
 Entrada Comprimento de **nome de usuário* em caracteres.  
  
 *Autenticação*  
 Entrada Cadeia de caracteres de autenticação (normalmente a senha).  
  
 *NameLength3*  
 Entrada Comprimento de **autenticação* em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando o **SQLConnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *identificador* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLConnect** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não oferecia suporte ao valor especificado do argumento *ValuePtr* em **SQLSetConnectAttr** e substituiu um valor semelhante. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de estabelecer conexão|O driver não pôde estabelecer uma conexão com a fonte de dados.|  
|08002|Nome da conexão em uso|(DM) o *ConnectionHandle* especificado já foi usado para estabelecer uma conexão com uma fonte de dados e a conexão ainda estava aberta ou o usuário estava procurando uma conexão.|  
|08004|O servidor rejeitou a conexão|A fonte de dados rejeitou o estabelecimento da conexão para motivos definidos pela implementação.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver estava tentando se conectar falhou antes da função concluir o processamento.|  
|28000|Especificação de autorização inválida|O valor especificado para o argumento *username* ou o valor especificado para a *autenticação* de argumento violou restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) o Gerenciador de driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função **SQLConnect** foi chamada e, antes de concluir a execução, a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle*e, em seguida, a função **SQLConnect** foi chamada novamente no *ConnectionHandle*.<br /><br /> Ou, a função **SQLConnect** foi chamada e, antes de concluir a execução, **SQLCancelHandle** foi chamado no *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *NameLength1*, *NameLength2*ou *NameLength3* era menor que 0, mas não igual a SQL_NTS.<br /><br /> (DM) o valor especificado para o argumento *NameLength1* excedeu o comprimento máximo para um nome de fonte de dados.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da conclusão da conexão com a fonte de dados. O período de tempo limite é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|O driver não dá suporte à execução de função assíncrona de nível de conexão|(DM) o aplicativo habilitou a operação assíncrona no identificador de conexão antes de fazer a conexão. No entanto, o driver não oferece suporte a operações assíncronas no identificador de conexão.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver especificado pelo nome da fonte de dados não oferece suporte à função.|  
|IM002|Fonte de dados não encontrada e nenhum driver padrão especificado|(DM) o nome da fonte de dados especificado no argumento *ServerName* não foi encontrado nas informações do sistema, nem havia uma especificação de driver padrão.|  
|IM003|O driver especificado não pôde ser conectado a|(DM) o driver listado na especificação de fonte de dados nas informações do sistema não foi encontrado ou não pôde ser conectado por algum outro motivo.|  
|IM004|Falha no SQLAllocHandle do driver em SQL_HANDLE_ENV|(DM) durante o **SQLConnect**, o Gerenciador de driver chamou a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_ENV e o driver retornou um erro.|  
|IM005|Falha no SQLAllocHandle do driver em SQL_HANDLE_DBC|(DM) durante o **SQLConnect**, o Gerenciador de driver chamou a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_DBC e o driver retornou um erro.|  
|IM006|Falha no SQLSetConnectAttr do driver|Durante o **SQLConnect**, o Gerenciador de driver chamou a função **SQLSetConnectAttr** do driver e o driver retornou um erro. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|IM009|Não é possível conectar à DLL de tradução|O driver não pôde se conectar à DLL de tradução que foi especificada para a fonte de dados.|  
|IM010|O nome da fonte de dados é muito longo|(DM) * \* ServerName* foi maior do que SQL_MAX_DSN_LENGTH caracteres.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o driver e o aplicativo|(DM) 32-o aplicativo de bits usa um DSN que se conecta a um driver de 64 bits; ou vice-versa.|  
|IM015|Falha na SQL_HANDLE_DBC_INFO_HANDLE do SQLConnect do driver|Se um driver retornar SQL_ERROR, o Gerenciador de driver retornará SQL_ERROR ao aplicativo e a conexão falhará.<br /><br /> Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
|S1118|O driver não oferece suporte à notificação assíncrona|Quando o driver não dá suporte à notificação assíncrona, não é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre por que um aplicativo usa o **SQLConnect**, consulte [conectando-se ao SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 O Gerenciador de driver não se conecta a um driver até que o aplicativo chame uma função (**SQLConnect**, **SQLDriverConnect**ou **SQLBrowseConnect**) para se conectar ao driver. Até esse ponto, o Gerenciador de driver funciona com seus próprios identificadores e gerencia as informações de conexão. Quando o aplicativo chama uma função de conexão, o Gerenciador de driver verifica se um driver está atualmente conectado para o *ConnectionHandle*especificado:  
  
-   Se um driver não estiver conectado ao, o Gerenciador de driver se conectará ao driver e chamará **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV, **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC, **SQLSetConnectAttr** (se o aplicativo especificou qualquer atributo de conexão) e a função de conexão no driver. O Gerenciador de driver retorna SQLSTATE IM006 (falha de **SQLSetConnectOption** do driver) e SQL_SUCCESS_WITH_INFO para a função de conexão se o driver retornou um erro para **SQLSetConnectAttr**. Para obter mais informações, consulte [conectando-se a uma fonte de dados ou driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md).  
  
-   Se o driver especificado já estiver conectado ao no *ConnectionHandle*, o Gerenciador de driver chamará apenas a função de conexão no driver. Nesse caso, o driver deve garantir que todos os atributos de conexão do *ConnectionHandle* mantenham suas configurações atuais.  
  
-   Se um driver diferente estiver conectado ao, o Gerenciador de driver chamará **SQLFreeHandle** com um *handletype* de SQL_HANDLE_DBC e, se nenhum outro driver estiver conectado a nesse ambiente, ele chamará **SQLFreeHandle** com um *identificador* de SQL_HANDLE_ENV no driver conectado e, em seguida, desconectará esse driver. Em seguida, ele executa as mesmas operações que quando um driver não está conectado ao.  
  
 Em seguida, o driver aloca identificadores e inicializa a si mesmo.  
  
 Quando o aplicativo chama **SQLDisconnect**, o Gerenciador de driver chama **SQLDisconnect** no driver. No entanto, ele não desconecta o driver. Isso mantém o driver na memória para aplicativos que se conectam repetidamente e se desconectam de uma fonte de dados. Quando o aplicativo chama **SQLFreeHandle** com um *handletype* de SQL_HANDLE_DBC, o Gerenciador de driver chama **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC e, em seguida, **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_ENV no driver e, em seguida, desconecta o driver.  
  
 Um aplicativo ODBC pode estabelecer mais de uma conexão.  
  
## <a name="driver-manager-guidelines"></a>Diretrizes do Gerenciador de driver  
 O conteúdo de **ServerName* afeta como o Gerenciador de driver e um driver funcionam juntos para estabelecer uma conexão com uma fonte de dados.  
  
-   Se \* *ServerName* contiver um nome de fonte de dados válido, o Gerenciador de driver localizará a especificação de fonte de dados correspondente nas informações do sistema e se conectará ao driver associado. O Gerenciador de driver passa cada argumento **SQLConnect** para o driver.  
  
-   Se o nome da fonte de dados não puder ser encontrado ou *ServerName* for um ponteiro nulo, o Gerenciador de driver localizará a especificação de fonte de dados padrão e se conectará ao driver associado. O Gerenciador de driver passa para o driver o *nome de usuário* e os argumentos de *autenticação* não modificados e "padrão" para o argumento *ServerName* .  
  
-   Se o argumento *ServerName* for "default", o Gerenciador de driver localizará a especificação de fonte de dados padrão e se conectará ao driver associado. O Gerenciador de driver passa cada argumento **SQLConnect** para o driver.  
  
-   Se o nome da fonte de dados não puder ser encontrado ou *ServerName* for um ponteiro nulo e a especificação de fonte de dados padrão não existir, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE IM002 (nome da fonte de dados não encontrado e nenhum driver padrão especificado).  
  
 Depois que ele é conectado pelo Gerenciador de driver, um driver pode localizar sua especificação de fonte de dados correspondente nas informações do sistema e usar informações específicas do driver da especificação para concluir seu conjunto de informações de conexão necessárias.  
  
 Se uma biblioteca de tradução padrão for especificada nas informações do sistema para a fonte de dados, o driver se conectará a ela. Uma biblioteca de tradução diferente pode ser conectada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_LIB. Uma opção de conversão pode ser especificada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Se um driver oferecer suporte a **SQLConnect**, a seção de palavra-chave do driver das informações do sistema para o driver deverá conter a palavra-chave **ConnectFunctions** com o primeiro conjunto de caracteres para "Y".  
  
### <a name="connection-pooling"></a>Pool de conexões  
 O pooling de conexões permite que um aplicativo reutilize uma conexão que já foi criada. Quando o pool de conexões está habilitado e o **SQLConnect** é chamado, o Gerenciador de driver tenta fazer a conexão usando uma conexão que faz parte de um pool de conexões em um ambiente designado para o pool de conexões. Esse ambiente é um ambiente compartilhado que é usado por todos os aplicativos que usam as conexões no pool.  
  
 O pool de conexões é habilitado antes de o ambiente ser alocado chamando **SQLSetEnvAttr** para definir SQL_ATTR_CONNECTION_POOLING como SQL_CP_ONE_PER_DRIVER (que especifica um máximo de um pool por driver) ou SQL_CP_ONE_PER_HENV (que especifica um máximo de um pool por ambiente). **SQLSetEnvAttr** nesse caso é chamado com *EnvironmentHandle* definido como NULL, o que torna o atributo um atributo de nível de processo. Se SQL_ATTR_CONNECTION_POOLING for definido como SQL_CP_OFF, o pool de conexões será desabilitado.  
  
 Depois que o pool de conexões tiver sido habilitado, **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV será chamado para alocar um ambiente. O ambiente alocado por essa chamada é um ambiente compartilhado porque o pool de conexões foi habilitado. No entanto, o ambiente que será usado não será determinado até que **SQLAllocHandle** com um *handletype* de SQL_HANDLE_DBC seja chamado.  
  
 **SQLAllocHandle** com um *handletype* de SQL_HANDLE_DBC é chamado para alocar uma conexão. O Gerenciador de driver tenta encontrar um ambiente compartilhado existente que corresponda aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existir, um será criado como um *ambiente compartilhado*implícito. Se um ambiente compartilhado correspondente for encontrado, o identificador de ambiente será retornado ao aplicativo e sua contagem de referência será incrementada.  
  
 No entanto, a conexão que será usada não será determinada até que **SQLConnect** seja chamado. Nesse ponto, o Gerenciador de driver tenta encontrar uma conexão existente no pool de conexões que corresponde aos critérios solicitados pelo aplicativo. Esses critérios incluem as opções de conexão solicitadas na chamada para **SQLConnect** (os valores das palavras-chave *ServerName*, *username*e *Authentication* ) e todos os atributos de conexão definidos desde que **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC foi chamado. O Gerenciador de driver verifica esses critérios em relação às palavras-chave de conexão correspondentes e aos atributos em conexões no pool. Se uma correspondência for encontrada, a conexão no pool será usada. Se nenhuma correspondência for encontrada, uma nova conexão será criada.  
  
 Se o atributo de ambiente SQL_ATTR_CP_MATCH for definido como SQL_CP_STRICT_MATCH, a correspondência deverá ser exata para que uma conexão no pool seja usada. Se o atributo de ambiente SQL_ATTR_CP_MATCH for definido como SQL_CP_RELAXED_MATCH, as opções de conexão na chamada para **SQLConnect** deverão corresponder, mas nem todos os atributos de conexão deverão corresponder.  
  
 As regras a seguir são aplicadas quando um atributo de conexão, conforme definido pelo aplicativo antes da chamada de **SQLConnect** , não corresponde ao atributo de conexão da conexão no pool:  
  
-   Se o atributo de conexão deve ser definido antes da conexão ser estabelecida:  
  
     Se SQL_ATTR_CP_MATCH for SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE na conexão em pool deverá ser idêntico ao atributo definido pelo aplicativo. Se SQL_CP_RELAXED_MATCH, os valores de SQL_ATTR_PACKET_SIZE podem ser diferentes.  
  
     O valor de SQL_ATTR_LOGIN_VALUE não afeta a correspondência.  
  
-   Se o atributo de conexão puder ser definido antes ou depois da conexão ser feita:  
  
     Se o atributo de conexão não tiver sido definido pelo aplicativo, mas tiver sido definido na conexão no pool e houver um padrão, o atributo de conexão na conexão em pool será definido de volta para o padrão e uma correspondência será declarada. Se não houver nenhum padrão, a conexão em pool não será considerada uma correspondência.  
  
     Se o atributo de conexão tiver sido definido pelo aplicativo, mas não tiver sido definido na conexão no pool, o atributo de conexão no pool será alterado para definido pelo aplicativo e uma correspondência será declarada.  
  
     Se o atributo de conexão tiver sido definido pelo aplicativo e também tiver sido definido na conexão no pool, mas os valores forem diferentes, o valor do atributo de conexão do aplicativo será usado e uma correspondência será declarada.  
  
-   Se os valores de atributos de conexão específicos do driver não forem idênticos e SQL_ATTR_CP_MATCH for definido como SQL_CP_STRICT_MATCH, a conexão no pool não será usada.  
  
 Quando o aplicativo chama **SQLDisconnect** para se desconectar, a conexão é retornada ao pool de conexões e está disponível para reutilização.  
  
### <a name="optimizing-connection-pooling-performance"></a>Otimizando o desempenho do pool de conexões  
 Quando transações distribuídas estão envolvidas, é possível otimizar o desempenho do pool de conexões usando **SQL_DTC_TRANSITION_COST**, que é um BITMASK SQLUINTEGER. As transições referenciadas são as transições do atributo de conexão SQL_ATTR_ENLIST_IN_DTC passar do valor 0 para diferente de zero e vice-versa. Essa é uma conexão de não inscrito em uma transação distribuída para inscrito em uma transação distribuída, e vice-versa. Dependendo de como o driver implementou a inscrição (definindo o atributo de conexão SQL_ATTR_ENLIST_IN_DTC), essas transições podem ser caras e, portanto, devem ser evitadas para melhor desempenho.  
  
 O valor retornado pelo driver contém qualquer combinação dos seguintes bits:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, quando definido, implica que a transição de zero para zero é significativamente mais cara do que uma transição de zero para outro valor diferente de zero (inscrevendo uma conexão previamente enlistada em sua próxima transação).  
  
-   O **SQL_DTC_UNENLIST_EXPENSIVE**, quando definido, implica que a transição de zero para nenhuma é significativamente mais cara do que usar uma conexão cujo atributo SQL_ATTR_ENLIST_IN_DTC já está definido como zero.  
  
 Há uma compensação de desempenho versus uso da conexão. Se um driver indicar que uma ou mais dessas transições são caras, o pool de conexões do Gerenciador de driver responderá a isso mantendo mais conexões no pool. Algumas das conexões no pool são preferenciais para uso não transacional e algumas são preferenciais para uso transacional. No entanto, se o driver indicar que essas transições não são dispendiosas, menos conexões poderão ser usadas, talvez alternando entre o uso não transacional e de transação.  
  
 Os drivers que não dão suporte a SQL_ATTR_ENLIST_IN_DTC não precisam dar suporte a SQL_DTC_TRANSITION_COST. Para drivers que dão suporte a SQL_ATTR_ENLIST_IN_DTC mas não SQL_DTC_TRANSITION_COST, presume-se que as transições não sejam caras, como se o driver retornasse 0 (nenhum conjunto de bits) para esse valor.  
  
 Embora SQL_DTC_TRANSITION_COST tenha sido introduzido no ODBC 3,5, um ODBC 2. o driver *x* também pode oferecer suporte a ele porque o Gerenciador de driver consultará essas informações, independentemente da versão do driver.  
  
### <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo aloca identificadores de ambiente e conexão. Em seguida, ele se conecta à fonte de dados SalesOrders com a ID de usuário JohnS e a senha Sesame e processa os dados. Quando o processamento de dados é concluído, ele se desconecta da fonte de dados e libera os identificadores.  
  
```cpp  
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
|Descobrindo e enumerando os valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Desconectando de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma cadeia de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
