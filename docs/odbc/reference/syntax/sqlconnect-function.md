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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab0a31845efeb484c554a9c9cf1afeaeab1a8bea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301212"
---
# <a name="sqlconnect-function"></a>Função SQLConnect
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLConnect** estabelece conexões com um driver e uma fonte de dados. O cabo de conexão faz referências ao armazenamento de todas as informações sobre a conexão com a fonte de dados, incluindo status, estado de transação e informações de erro.  
  
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
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *Servername*  
 [Entrada] Nome da fonte dos dados. Os dados podem estar localizados no mesmo computador do programa, ou em outro computador em algum lugar em uma rede. Para obter informações sobre como um aplicativo escolhe uma fonte de dados, consulte [Escolher uma Fonte de Dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Entrada] Comprimento de **ServerName* em caracteres.  
  
 *Username*  
 [Entrada] Identificador de usuário.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento de **UserName* em caracteres.  
  
 *Autenticação*  
 [Entrada] Seqüência de autenticação (tipicamente a senha).  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento de **Autenticação* em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLConnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *alça* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLConnect** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não suportava o valor especificado do argumento *ValuePtr* no **SQLSetConnectAttr** e substituiu um valor semelhante. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de estabelecer conexão|O motorista não conseguiu estabelecer uma conexão com a fonte de dados.|  
|08002|Nome de conexão em uso|(DM) O *ConnectionHandle* especificado já havia sido usado para estabelecer uma conexão com uma fonte de dados, e a conexão ainda estava aberta ou o usuário estava navegando por uma conexão.|  
|08004|Servidor rejeitou a conexão|A fonte de dados rejeitou o estabelecimento da conexão por razões definidas pela implementação.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o motorista estava tentando se conectar falhou antes que a função concluísse o processamento.|  
|28000|Especificação de autorização inválida|O valor especificado para o argumento *UserName* ou o valor especificado para o argumento *Autenticação* violou restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) O Driver Manager não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função **SQLConnect** foi chamada e, antes de ser concluída, [a função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle*e, em seguida, a função **SQLConnect** foi chamada novamente no *ConnectionHandle*.<br /><br /> Ou, a função **SQLConnect** foi chamada e, antes de ser concluída, o **SQLCancelHandle** foi chamado no *ConnectionHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava sendo executada quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para o argumento *NameLength1,* *NameLength2*ou *NameLength3* foi menor que 0, mas não igual a SQL_NTS.<br /><br /> (DM) O valor especificado para o argumento *NameLength1* excedeu o comprimento máximo de um nome de origem de dados.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes da conexão com a fonte de dados concluída. O período de tempo é definido através de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|Driver não suporta execução de função assíncrona nível de conexão|(DM) O aplicativo habilitou a operação assíncrona no cabo de conexão antes de fazer a conexão. No entanto, o driver não suporta operações assíncronas no cabo de conexão.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver especificado pelo nome da fonte de dados não suporta a função.|  
|IM002|Fonte de dados não encontrada e nenhum driver padrão especificado|(DM) O nome de origem dos dados especificado no argumento *ServerName* não foi encontrado nas informações do sistema, nem havia uma especificação padrão do driver.|  
|IM003|Driver especificado não poderia ser conectado a|(DM) O driver listado na especificação de origem de dados nas informações do sistema não foi encontrado ou não pôde ser conectado por algum outro motivo.|  
|IM004|SQLAllocHandle do driver em SQL_HANDLE_ENV falhou|(DM) Durante o **SQLConnect,** o Driver Manager ligou para a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_ENV e o motorista retornou um erro.|  
|IM005|SQLAllocHandle do motorista no SQL_HANDLE_DBC falhou|(DM) Durante o **SQLConnect,** o Driver Manager ligou para a função **SQLAllocHandle** do driver com um *HandleType* de SQL_HANDLE_DBC e o motorista retornou um erro.|  
|IM006|Falha no SQLSetConnectAttr do driver|Durante **o SQLConnect,** o Driver Manager ligou para a função **SQLSetConnectAttr** do driver e o driver retornou um erro. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|IM009|Não é possível se conectar à tradução DLL|O driver não pôde se conectar à DLL de tradução especificada para a fonte de dados.|  
|IM010|Nome de origem de dados muito longo|(DM) * \*ServerName* foi mais longo do que SQL_MAX_DSN_LENGTH caracteres.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o Driver e o Aplicativo|(DM) O aplicativo de 32 bits usa uma conexão DSN a um driver de 64 bits; ou vice-versa.|  
|IM015|Falha no SQLConnect do driver na SQL_HANDLE_DBC_INFO_HANDLE|Se um motorista retornar SQL_ERROR, o Gerenciador de Driver retornará SQL_ERROR ao aplicativo e a conexão falhará.<br /><br /> Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [Developing Connection-Pool Awareness em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
|S1118|O driver não suporta notificação assíncrona|Quando o driver não suporta notificação assíncrona, não é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre por que um aplicativo usa **SQLConnect,** consulte [Conectando com sqlconnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 O Driver Manager não se conecta a um driver até que o aplicativo chame uma função **(SQLConnect,** **SQLDriverConnect**ou **SQLBrowseConnect)** para se conectar ao driver. Até esse ponto, o Driver Manager trabalha com suas próprias alças e gerencia as informações de conexão. Quando o aplicativo chama uma função de conexão, o Gerenciador de driver verifica se um driver está conectado atualmente para o *ConnectionHandle*especificado :  
  
-   Se um driver não estiver conectado, o Driver Manager se conecta ao driver e chama **o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV, **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC, **SQLSetConnectAttr** (se o aplicativo especificar quaisquer atributos de conexão) e a função de conexão no driver. O Driver Manager retorna o SQLSTATE IM006 (falha no **SQLSetConnectOption** do driver) e SQL_SUCCESS_WITH_INFO para a função de conexão se o driver retornou um erro para **SQLSetConnectAttr**. Para obter mais informações, consulte [Conectar-se a uma fonte de dados ou driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md).  
  
-   Se o driver especificado já estiver conectado no *ConnectionHandle,* o Gerenciador de drivers chamará apenas a função de conexão no driver. Neste caso, o driver deve certificar-se de que todos os atributos de conexão para o *ConnectionHandle* mantenham suas configurações atuais.  
  
-   Se um driver diferente estiver conectado, o Driver Manager liga para **o SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC e, em seguida, se nenhum outro driver estiver conectado nesse ambiente, ele chamará **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_ENV no driver conectado e, em seguida, desconecta o driver. Em seguida, ele executa as mesmas operações que quando um driver não está conectado.  
  
 O motorista então aloca as alças e se inicializa.  
  
 Quando o aplicativo chama **SQLDisconnect,** o Driver Manager chama **SQLDisconnect** no driver. No entanto, ele não desconecta o driver. Isso mantém o driver na memória para aplicativos que se conectam repetidamente e se desconectam de uma fonte de dados. Quando o aplicativo chama **sQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC, o Gerenciador de driver liga para **o SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DBC e, em seguida, **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_ENV no driver e, em seguida, desconecta o driver.  
  
 Um aplicativo ODBC pode estabelecer mais de uma conexão.  
  
## <a name="driver-manager-guidelines"></a>Diretrizes do Driver Manager  
 O conteúdo do **ServerName* afeta a forma como o Driver Manager e um driver trabalham juntos para estabelecer uma conexão com uma fonte de dados.  
  
-   Se \* *ServerName* contiver um nome de origem de dados válido, o Gerenciador de driver seleção localizará a especificação correspondente da fonte de dados nas informações do sistema e se conectará ao driver associado. O Driver Manager passa cada argumento **SQLConnect** para o driver.  
  
-   Se o nome da fonte de dados não puder ser encontrado ou *ServerName* for um ponteiro nulo, o Gerenciador de driver satisfaz a especificação de origem de dados padrão e se conecta ao driver associado. O Driver Manager passa para o driver os argumentos Nome de *usuário* e *autenticação* não modificados e "DEFAULT" para o argumento *ServerName.*  
  
-   Se o argumento *ServerName* for "DEFAULT", o Gerenciador de driver seleção localizará a especificação de origem de dados padrão e se conectará ao driver associado. O Driver Manager passa cada argumento **SQLConnect** para o driver.  
  
-   Se o nome da fonte de dados não puder ser encontrado ou *serverName* for um ponteiro nulo e a especificação de origem de dados padrão não existir, o Gerenciador de driver retorna SQL_ERROR com O SQLSTATE IM002 (nome de origem de dados não encontrado e nenhum driver padrão especificado).  
  
 Depois de conectado pelo Driver Manager, o driver pode localizar sua especificação de origem de dados correspondente nas informações do sistema e usar informações específicas do driver a partir da especificação para completar seu conjunto de informações de conexão necessárias.  
  
 Se uma biblioteca de tradução padrão for especificada nas informações do sistema para a fonte de dados, o driver se conectará a ela. Uma biblioteca de tradução diferente pode ser conectada ligando para **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_LIB. Uma opção de tradução pode ser especificada ligando para **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Se um driver suportar **o SQLConnect,** a seção de palavras-chave do driver deve conter a palavra-chave **ConnectFunctions** com o primeiro caractere definido como "Y".  
  
### <a name="connection-pooling"></a>Pool de conexões  
 O pool de conexões permite que um aplicativo reutilize uma conexão que já foi criada. Quando o pool de conexões é ativado e o **SQLConnect** é chamado, o Driver Manager tenta fazer a conexão usando uma conexão que faz parte de um pool de conexões em um ambiente designado para pool de conexões. Este ambiente é um ambiente compartilhado que é usado por todos os aplicativos que usam as conexões na piscina.  
  
 O pool de conexões é ativado antes que o ambiente seja alocado ligando para **sqlsetEnvAttr** para definir SQL_ATTR_CONNECTION_POOLING para SQL_CP_ONE_PER_DRIVER (que especifica um máximo de um pool por driver) ou SQL_CP_ONE_PER_HENV (que especifica um máximo de um pool por ambiente). **SQLSetEnvAttr** neste caso é chamado com *EnvironmentHandle* definido como nulo, o que torna o atributo um atributo de nível de processo. Se SQL_ATTR_CONNECTION_POOLING estiver definido como SQL_CP_OFF, o pool de conexões será desativado.  
  
 Depois que o pool de conexões for ativado, **o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV é chamado para alocar um ambiente. O ambiente alocado por esta chamada é um ambiente compartilhado porque o pool de conexões foi ativado. No entanto, o ambiente que será usado não é determinado até que **o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC seja chamado.  
  
 **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC é chamado para alocar uma conexão. O Gerenciador de drivers tenta encontrar um ambiente compartilhado existente que corresponda aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existe, um deles é criado como um *ambiente compartilhado*implícito. Se um ambiente compartilhado correspondente for encontrado, a alça do ambiente será devolvida ao aplicativo e sua contagem de referência será incrementada.  
  
 No entanto, a conexão que será usada não é determinada até que **o SQLConnect** seja chamado. Nesse ponto, o Driver Manager tenta encontrar uma conexão existente no pool de conexão que corresponda aos critérios solicitados pelo aplicativo. Esses critérios incluem as opções de conexão solicitadas na chamada para **SQLConnect** (os valores das palavras-chave *ServerName,* *UserName*e *Authentication)* e quaisquer atributos de conexão definidos desde **que o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC foi chamado. O Driver Manager verifica esses critérios com as palavras-chave e atributos de conexão correspondentes em conexões no pool. Se uma correspondência for encontrada, a conexão na piscina é usada. Se nenhuma correspondência for encontrada, uma nova conexão será criada.  
  
 Se o atributo do ambiente SQL_ATTR_CP_MATCH estiver definido como SQL_CP_STRICT_MATCH, a correspondência deve ser exata para que uma conexão no pool seja usada. Se o atributo do ambiente SQL_ATTR_CP_MATCH estiver definido como SQL_CP_RELAXED_MATCH, as opções de conexão na chamada para **SQLConnect** devem corresponder, mas nem todos os atributos de conexão devem corresponder.  
  
 As seguintes regras são aplicadas quando um atributo de conexão, definido pelo aplicativo antes de ser chamado **pelo SQLConnect,** não corresponde ao atributo de conexão da conexão no pool:  
  
-   Se o atributo de conexão deve ser definido antes da conexão ser feita:  
  
     Se SQL_ATTR_CP_MATCH for SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE na conexão agrupada deve ser idêntica ao atributo definido pelo aplicativo. Se SQL_CP_RELAXED_MATCH, os valores de SQL_ATTR_PACKET_SIZE podem ser diferentes.  
  
     O valor da SQL_ATTR_LOGIN_VALUE não afeta a partida.  
  
-   Se o atributo de conexão puder ser definido antes ou depois de a conexão ser feita:  
  
     Se o atributo de conexão não tiver sido definido pelo aplicativo, mas tiver sido definido na conexão no pool e houver um padrão, o atributo de conexão na conexão agrupada será definido de volta ao padrão e uma correspondência é declarada. Se não houver padrão, a conexão agrupada não é considerada compatível.  
  
     Se o atributo de conexão tiver sido definido pelo aplicativo, mas não tiver sido definido na conexão no pool, o atributo de conexão no pool será alterado para o definido pelo aplicativo e uma correspondência será declarada.  
  
     Se o atributo de conexão tiver sido definido pelo aplicativo e também tiver sido definido na conexão no pool, mas os valores forem diferentes, o valor do atributo de conexão do aplicativo será usado e uma correspondência será declarada.  
  
-   Se os valores dos atributos de conexão específicos do driver não forem idênticos e SQL_ATTR_CP_MATCH for definido como SQL_CP_STRICT_MATCH, a conexão no pool não será usada.  
  
 Quando o aplicativo chama **SQLDisconnect** para desconectar, a conexão é devolvida ao pool de conexão e está disponível para reutilização.  
  
### <a name="optimizing-connection-pooling-performance"></a>Otimização do desempenho do pool de conexões  
 Quando as transações distribuídas estão envolvidas, é possível otimizar o desempenho de pooling de conexões usando **SQL_DTC_TRANSITION_COST**, que é uma máscara de bitS. As transições referidas são as transições do atributo de conexão SQL_ATTR_ENLIST_IN_DTC indo do valor 0 para o não zero, e vice-versa. Esta é uma conexão que vai de não alistar em uma transação distribuída para alistado em uma transação distribuída, e vice-versa. Dependendo de como o driver implementou o alistamento (definição do atributo de conexão SQL_ATTR_ENLIST_IN_DTC), essas transições podem ser caras e, portanto, devem ser evitadas para o melhor desempenho.  
  
 O valor devolvido pelo driver contém qualquer combinação dos seguintes bits:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, quando definido, implica que a transição de zero a não-zero é significativamente mais cara do que uma transição de não zero para outro valor não zero (alistando uma conexão previamente alistada em sua próxima transação).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, quando definido, implica que a transição não zero a zero é significativamente mais cara do que usar uma conexão cujo SQL_ATTR_ENLIST_IN_DTC atributo já está definido como zero.  
  
 Há uma troca de desempenho versus uso de conexão. Se um driver indicar que uma ou mais dessas transições são caras, o pooler de conexões do gerenciador de driver responde a isso mantendo mais conexões no pool. Algumas das conexões no pool são preferidas para uso não transacional, e algumas são preferidas para uso transacional. No entanto, se o driver indicar que essas transições não são caras, menos conexões podem ser usadas, talvez alternando entre uso não transacional e transacional.  
  
 Os motoristas que não suportam SQL_ATTR_ENLIST_IN_DTC não precisam suportar SQL_DTC_TRANSITION_COST. Para os motoristas que suportam SQL_ATTR_ENLIST_IN_DTC mas não SQL_DTC_TRANSITION_COST, presume-se que as transições não são caras, como se o motorista devolvesse 0 (sem bits definidos) por esse valor.  
  
 Embora SQL_DTC_TRANSITION_COST tenha sido introduzido no ODBC 3.5, um ODBC 2. *x* driver também pode apoiá-lo porque o gerenciador do driver irá consultar essas informações independentemente da versão do driver.  
  
### <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo aloca o ambiente e as alças de conexão. Em seguida, ele se conecta à fonte de dados SalesOrders com o ID do usuário JohnS e a senha Sesame e processa dados. Quando termina o processamento de dados, ele se desconecta da fonte de dados e libera as alças.  
  
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
|Alocando uma alça|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Descobrir e enumerar valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Desconectando-se de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma seqüência de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
