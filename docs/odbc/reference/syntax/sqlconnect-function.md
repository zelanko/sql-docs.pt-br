---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 530a5acf9cc7c0de375906279aff2bc6a05ec8a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259533"
---
# <a name="sqlconnect-function"></a>Função SQLConnect
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLConnect** estabelece conexões com um driver e uma fonte de dados. O armazenamento de referências do identificador de conexão de todas as informações sobre a conexão à fonte de dados, incluindo status, o estado de transação e informações de erro.  
  
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
 *ConnectionHandle*  
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
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLConnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DBC e uma *manipular* dos *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLConnect** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O driver não oferecia suporte para o valor especificado do *ValuePtr* argumento **SQLSetConnectAttr** e substituído, um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08001|Não é possível estabelecer conexão de cliente|O driver não pôde estabelecer uma conexão com a fonte de dados.|  
|08002|Nome da Conexão em uso|(DM) especificado *ConnectionHandle* já foi usado para estabelecer uma conexão com uma fonte de dados e a conexão foram aberta ou o usuário estava navegando para uma conexão.|  
|08004|O servidor recusou a conexão|A fonte de dados rejeitados o estabelecimento da conexão por motivos de implementação definida.|  
|08S01|Falha de link de comunicação|Falha no link de comunicação entre o driver e a fonte de dados ao qual o driver estava tentando conectar-se antes do processamento da função foi concluída.|  
|28000|Especificação de autorização inválida|O valor especificado para o argumento *nome de usuário* ou o valor especificado para o argumento *autenticação* violou as restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O Gerenciador de Driver (DM) não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. O **SQLConnect** função foi chamada e antes ele concluiu a execução, [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado no *ConnectionHandle*e, em seguida, o **SQLConnect** a função foi chamada novamente na *ConnectionHandle*.<br /><br /> Ou, o **SQLConnect** função foi chamada e antes ele concluiu a execução, **SQLCancelHandle** foi chamado no *ConnectionHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona (não desse último) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *NameLength1*, *NameLength2*, ou *NameLength3* era menor que 0, mas não é igual a SQL_NTS.<br /><br /> (DM) o valor especificado para o argumento *NameLength1* excedeu o comprimento máximo para um nome de fonte de dados.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da conexão à fonte de dados concluída. O período de tempo limite é definido por meio **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|Driver não oferece suporte à execução de função assíncrona de nível de conexão|(DM) o aplicativo ativado a operação assíncrona no identificador da conexão antes de fazer a conexão. No entanto, o driver não oferece suporte a operações assíncronas no identificador de conexão.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) o driver especificado pelo nome de fonte de dados não suporta a função.|  
|IM002|Fonte de dados não encontrado e nenhum driver padrão especificado|(DM) a fonte de dados especificado no argumento de nome *ServerName* não foi encontrada nas informações do sistema, nem existia uma especificação de driver padrão.|  
|IM003|Driver especificado não foi possível se conectar ao|O driver de (DM) listados nos dados de especificação de fonte de informações do sistema não foi encontrada ou não pôde ser conectada por algum outro motivo.|  
|IM004|Falha de SQLAllocHandle do driver em SQL_HANDLE_ENV|(DM) durante **SQLConnect**, o Gerenciador de Driver chamado do driver **SQLAllocHandle** funcionar com um *HandleType* de SQL_HANDLE_ENV e o driver retornou um erro.|  
|IM005|Falha de SQLAllocHandle do driver em SQL_HANDLE_DBC|(DM) durante **SQLConnect**, o Gerenciador de Driver chamado do driver **SQLAllocHandle** funcionar com um *HandleType* de SQL_HANDLE_DBC e o driver retornou um erro.|  
|IM006|Falha de SQLSetConnectAttr do driver|Durante **SQLConnect**, o Gerenciador de Driver chamado do driver **SQLSetConnectAttr** função e o driver retornaram um erro. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|IM009|Não é possível conectar-se a DLL de conversão|O driver não pôde conectar-se à conversão de DLL que foi especificado para a fonte de dados.|  
|IM010|Nome de fonte de dados muito longo|(DM)  *\*ServerName* tinha mais de SQL_MAX_DSN_LENGTH caracteres.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o Driver e o aplicativo|Aplicativo de 32 bits (DM) usa um DSN que se conectar a um driver de 64 bits. ou vice-versa.|  
|IM015|Falha SQLConnect do driver em SQL_HANDLE_DBC_INFO_HANDLE|Se um driver retornará SQL_ERROR, o Gerenciador de Driver retornará SQL_ERROR ao aplicativo e a conexão falhará.<br /><br /> Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
|S1118|Driver não oferece suporte a notificação assíncrona|Quando o driver não oferece suporte a notificação assíncrona, é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre por que um aplicativo usa **SQLConnect**, consulte [conectando com SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 O Gerenciador de Driver não se conecta a um driver até que o aplicativo chama uma função (**SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**) para conectar-se para o driver. Até esse ponto, o Gerenciador de Driver funciona com seus próprio alças e gerencia as informações de conexão. Quando o aplicativo chama uma função de conexão, o Gerenciador de Driver verifica se um driver está conectado atualmente à especificado *ConnectionHandle*:  
  
-   Se um driver não está conectado a, o Gerenciador de Driver conecta-se para o driver e chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV, **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC, **SQLSetConnectAttr** (se o aplicativo especificado quaisquer atributos de conexão) e a função de conexão no driver. O Gerenciador de Driver retornará SQLSTATE IM006 (motorista **SQLSetConnectOption** falha) e SQL_SUCCESS_WITH_INFO para a função de conexão se o driver retornou um erro para **SQLSetConnectAttr**. Para obter mais informações, consulte [conectando-se a uma fonte de dados ou Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md).  
  
-   Se o driver especificado já está conectado na *ConnectionHandle*, o Gerenciador de Driver chama apenas a função de conexão no driver. Nesse caso, o driver deve garantir que a conexão de todos os atributos para o *ConnectionHandle* manter suas configurações atuais.  
  
-   Se um driver diferente é conectado a, o Gerenciador de Driver chama **SQLFreeHandle** com um *HandleType* SQL_HANDLE_DBC, e em seguida, se nenhum outro driver estiver conectado nesse ambiente, ele chama **SQLFreeHandle** com um *HandleType* SQL_HANDLE_ENV no driver conectado e, em seguida, desconecta esse driver. Ele, em seguida, executa as mesmas operações quando um driver não está conectado a.  
  
 O driver, em seguida, aloca identificadores e inicializa a próprio.  
  
 Quando o aplicativo chama **SQLDisconnect**, as chamadas de Gerenciador de Driver **SQLDisconnect** no driver. No entanto, ele não desconecta o driver. Isso mantém o driver na memória para aplicativos que repetidamente, conectar e desconectar de uma fonte de dados. Quando o aplicativo chama **SQLFreeHandle** com um *HandleType* SQL_HANDLE_DBC, chama o Gerenciador de Driver **SQLFreeHandle** com um *HandleType*  SQL_HANDLE_DBC e, em seguida **SQLFreeHandle** com um *HandleType* SQL_HANDLE_ENV no driver e, em seguida, desconecta o driver.  
  
 Um aplicativo ODBC pode estabelecer mais de uma conexão.  
  
## <a name="driver-manager-guidelines"></a>Diretrizes do Gerenciador de driver  
 O conteúdo do **ServerName* afetam como o Gerenciador de Driver e um driver funcionam juntos para estabelecer uma conexão a uma fonte de dados.  
  
-   Se \* *ServerName* contém um nome de fonte de dados válido, o Gerenciador de Driver localiza a especificação de fonte de dados correspondentes nas informações do sistema e conecta-se para o driver associado. O Gerenciador de Driver passa cada **SQLConnect** argumento para o driver.  
  
-   Se o nome da fonte de dados não pode ser encontrado ou *ServerName* for um ponteiro nulo, o Gerenciador de Driver localiza a especificação de fonte de dados padrão e se conecta ao driver associado. O Gerenciador de Driver passa para o driver a *nome de usuário* e *autenticação* argumentos sem modificações e "DEFAULT" para o *ServerName* argumento.  
  
-   Se o *ServerName* argumento é "Padrão", o Gerenciador de Driver localiza a especificação de fonte de dados padrão e se conecta ao driver associado. O Gerenciador de Driver passa cada **SQLConnect** argumento para o driver.  
  
-   Se o nome da fonte de dados não pode ser encontrado ou *ServerName* é um ponteiro nulo e o padrão de especificação de fonte de dados não existir, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE IM002 (fonte de dados não padrão e o nome não encontrado driver especificado).  
  
 Depois que ele está conectado a pelo Gerenciador de Driver, um driver pode localizar sua especificação de fonte de dados correspondentes nas informações do sistema e usar informações específicas do driver da especificação para concluir seu conjunto de informações de conexão necessárias.  
  
 Se uma biblioteca de conversão padrão for especificada nas informações do sistema da fonte de dados, o driver se conecta a ele. Uma biblioteca de conversão diferentes pode ser conectada a chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_LIB. Uma opção de conversão pode ser especificada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Se um driver compatível com **SQLConnect**, a seção de palavra-chave driver as informações do sistema para o driver deve conter o **ConnectFunctions** palavra-chave com o primeiro caractere definido como "Y".  
  
### <a name="connection-pooling"></a>Pool de conexões  
 Pooling de Conexão permite que um aplicativo para reutilizar uma conexão que já foi criado. Quando o pooling de conexão está habilitado e **SQLConnect** é chamado, o Gerenciador de Driver tentará fazer a conexão usando uma conexão que faz parte de um pool de conexões em um ambiente que foi designado para o pool de conexão. Esse ambiente é um ambiente compartilhado que é usado por todos os aplicativos que usam as conexões no pool.  
  
 Pooling de Conexão está habilitado antes do ambiente é alocado chamando **SQLSetEnvAttr** definir SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER (que especifica um máximo de um pool por driver) ou SQL_CP_ONE_PER_HENV (que especifica um máximo de um pool por ambiente). **SQLSetEnvAttr** nesse caso é chamado com *EnvironmentHandle* definido como null, o que torna o atributo de um atributo de nível de processo. Se SQL_ATTR_CONNECTION_POOLING for definido como SQL_CP_OFF, pooling de conexão está desabilitada.  
  
 Depois que o pooling de conexão tiver sido habilitada, **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV é chamada para alocar um ambiente. O ambiente alocado por essa chamada é um ambiente compartilhado porque o pooling de conexão tiver sido habilitado. No entanto, o ambiente que será usado não é determinado até **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC é chamado.  
  
 **Falha de SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC é chamada para alocar uma conexão. O Gerenciador de Driver tenta encontrar um ambiente compartilhado existente que corresponde aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existir, será criado um como implícito *ambiente compartilhado*. Se um ambiente compartilhado correspondente for encontrado, o identificador de ambiente é retornado ao aplicativo e sua contagem de referência é incrementada.  
  
 No entanto, a conexão que será usado não é determinada até **SQLConnect** é chamado. Nesse ponto, o Gerenciador de Driver tenta localizar uma conexão existente no pool de conexão que corresponde aos critérios solicitados pelo aplicativo. Esses critérios incluem as opções de conexão solicitadas na chamada para **SQLConnect** (os valores de *ServerName*, *nome de usuário*, e  *Autenticação* palavras-chave) e os atributos de conexão definida desde **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC foi chamado. O Gerenciador de Driver verifica esses critérios contra os atributos em conexões no pool e palavras-chave de conexão correspondente. Se uma correspondência for encontrada, a conexão no pool é usado. Se nenhuma correspondência for encontrada, uma nova conexão será criada.  
  
 Se o atributo de ambiente SQL_ATTR_CP_MATCH é definido como SQL_CP_STRICT_MATCH, a correspondência deve ser exata para uma conexão no pool para ser usado. Se o atributo de ambiente SQL_ATTR_CP_MATCH é definido como SQL_CP_RELAXED_MATCH, a conexão opções na chamada para **SQLConnect** devem corresponder, mas não todos os atributos de conexão deve corresponder.  
  
 As seguintes regras são aplicadas quando um atributo de conexão, conforme definido pelo aplicativo antes de **SQLConnect** é chamado, não coincide com o atributo de conexão no pool de conexão:  
  
-   Se o atributo de conexão deve ser definido antes que a conexão seja feita:  
  
     Se SQL_ATTR_CP_MATCH for SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE em que a conexão em pool devem ser idênticos para o atributo definido pelo aplicativo. Se SQL_CP_RELAXED_MATCH, os valores de SQL_ATTR_PACKET_SIZE pode ser diferente.  
  
     O valor de SQL_ATTR_LOGIN_VALUE não afeta a correspondência.  
  
-   Se o atributo de conexão pode ser definido antes ou depois que a conexão é feita:  
  
     Se o atributo de conexão não foi definido pelo aplicativo, mas foi definido em que a conexão no pool, e há um padrão, o atributo de conexão em que a conexão em pool é definido de volta para o padrão e uma correspondência é declarada. Se não houver nenhum padrão, a conexão em pool não é considerado uma correspondência.  
  
     Se o atributo de conexão tiver sido definido pelo aplicativo, mas não foi definido em que a conexão no pool, o atributo de conexão no pool é alterado para esse conjunto pelo aplicativo e uma correspondência é declarada.  
  
     Se o atributo de conexão tiver sido definido pelo aplicativo e também foi definido em que a conexão no pool, mas os valores forem diferentes, o valor do atributo de conexão do aplicativo é usado e uma correspondência é declarada.  
  
-   Se os valores dos atributos de conexão específicos de driver não são idênticos e SQL_ATTR_CP_MATCH é definido como SQL_CP_STRICT_MATCH, a conexão no pool não será usado.  
  
 Quando o aplicativo chama **SQLDisconnect** para desconectar, a conexão é retornada ao pool de conexão e está disponível para reutilização.  
  
### <a name="optimizing-connection-pooling-performance"></a>Otimizando o desempenho do pool de Conexão  
 Quando as transações distribuídas estão envolvidas, é possível otimizar o desempenho do pool por meio de conexão **SQL_DTC_TRANSITION_COST**, que é um bitmask SQLUINTEGER. As transições conhecidas são as transições do atributo de conexão SQL_ATTR_ENLIST_IN_DTC mudar de valor 0 como não zero e vice-versa. Isso é uma conexão que vão do não inscrita em uma transação distribuída inscrita em uma transação distribuída e vice-versa. Dependendo de como o driver implementou inscrição (definir atributo de conexão SQL_ATTR_ENLIST_IN_DTC), essas transições podem ser caras e, portanto, devem ser evitadas para melhor desempenho.  
  
 O valor retornado pelo driver contém qualquer combinação destes bits:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, quando definido, implica que o zero para fazer a transição diferente de zero é significativamente mais caro do que uma transição de diferente de zero para outro valor diferente de zero (inscrever-se uma conexão anteriormente inscrito na sua próxima transação).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, quando definido, implica diferente de zero para zero transição é significativamente mais caro do que usar uma conexão cujo atributo SQL_ATTR_ENLIST_IN_DTC já está definido como zero.  
  
 Há um desempenho em relação ao equilíbrio de uso de conexão. Se um driver indica que um ou mais dessas transições são caros, o pooler de conexão do Gerenciador de driver responde a isso, mantendo mais conexões no pool. Algumas conexões no pool são preferenciais para uso não transacional, e alguns são preferenciais para uso transacional. No entanto, se o driver indica que essas transições não são caras, menos conexões podem ser usadas, talvez alternando entre não transacional e de uso transacional.  
  
 Drivers que não dão suporte a SQL_ATTR_ENLIST_IN_DTC não é necessário dar suporte a SQL_DTC_TRANSITION_COST. Para os drivers que dão suporte a SQL_ATTR_ENLIST_IN_DTC, mas não SQL_DTC_TRANSITION_COST, supõe-se que as transições não são caras, como se o driver retornou 0 (nenhum conjunto de bits) para esse valor.  
  
 Embora SQL_DTC_TRANSITION_COST foi introduzido no ODBC 3.5, um ODBC 2. *x* driver também der suporte a isso porque o Gerenciador de driver será consultar essas informações independentemente da versão do driver.  
  
### <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo aloca ambiente e conexão identificadores. Em seguida, ele se conecta à fonte de dados SalesOrders com o JohnS de ID de usuário e a senha Sesame e processa dados. Quando tiver concluído o processamento de dados, ele se desconecta da fonte de dados e libera os identificadores.  
  
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
|Conectando a uma fonte de dados usando uma caixa de diálogo ou de cadeia de caracteres de conexão|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
