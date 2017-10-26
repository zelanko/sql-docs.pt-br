---
title: "Operação de Driver de rastreamento | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e364f990cc2428d771f3bc57015df0636e23fbfb
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="tracing-driver-operation"></a>Operação de rastreamento de driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] suporta o uso de rastreamento (ou log) para ajudar a resolver problemas com o driver JDBC quando ele é usado em seu aplicativo. Para habilitar o uso de rastreamento, o driver JDBC usa as APIs de log no logging, que fornece um conjunto de classes para criar objetos de agente de log e LogRecord.  
  
> [!NOTE]  
>  Para o componente nativo (sqljdbc_xa.dll) que está incluído com o driver JDBC, o rastreamento é habilitado pela estrutura de Diagnósticos Internos (BID). Para obter informações sobre BID, consulte [rastreamento de acesso a dados no SQL Server](http://go.microsoft.com/fwlink/?LinkId=70042).  
  
 Quando você desenvolve seu aplicativo, você pode fazer chamadas para objetos de agente de log, que por sua vez, criam objetos LogRecord, que são então passados aos objetos de manipulador para processamento. Agente de log e o manipulador de ambos os níveis de log de uso de objetos e opcionalmente filtros de log, para regular quais LogRecords são processados. Quando as operações de log estiverem concluídas, os objetos do manipulador, opcionalmente, podem usar objetos de formatador para publicar as informações de log.  
  
 Por padrão, a estrutura do java.util.logging grava sua saída em um arquivo. Este arquivo de log de saída deve ter permissões de gravação para o contexto sob o qual o driver JDBC está executando.  
  
> [!NOTE]  
>  Para obter mais informações sobre como usar os vários objetos de log para rastreamento de programa, consulte a documentação do Java Logging APIs no site da Sun Microsystems.  
  
 As seções a seguir descrevem os níveis de log e as categorias que podem ser registradas em log, e fornecem informações sobre como habilitar rastreamento em seu aplicativo.  
  
## <a name="logging-levels"></a>Níveis de log  
 Toda mensagem de log que é criada tem um nível de log associado. O nível de log determina a importância da mensagem de log, que é definida como o **nível** classe Logging. Habilitar log em um nível também habilita log em todos os níveis mais altos. Esta seção descreve os níveis de log para categorias de log públicas e categorias de log internas. Para obter mais informações sobre categorias de log, consulte a seção Categorias de log neste tópico.  
  
 A tabela a seguir descreve cada nível de log disponível para categorias de log públicas.  
  
|Nome|Description|  
|----------|-----------------|  
|SEVERE|Indica uma falha séria e é o nível mais alto de log. No driver JDBC, este nível é usado para relatar erros e exceções.|  
|WARNING|Indica um problema potencial.|  
|INFO|Fornece mensagens informativas.|  
|CONFIG|Fornece mensagens de configuração. Observe que o driver JDBC atualmente não fornece nenhuma mensagem de configuração.|  
|FINE|Fornece informações básicas de rastreamento inclusive todas as exceções lançadas pelos métodos públicos.|  
|FINER|Fornece informações de rastreamento detalhadas inclusive todas as entradas de método público e pontos de saída com tipos de dados de parâmetro associados e todas as propriedades públicas para classes públicas. Além disso, parâmetro de entrada, parâmetros de saída e valores de retorno de método exceto CLOB, BLOB, NCLOB, Reader, \<fluxo > tipos de valor de retorno.|  
|FINEST|Fornece informações de rastreamento altamente detalhadas. Este é o nível mais baixo de log.|  
|OFF|Desliga o log.|  
|ALL|Habilita log de todas as mensagens.|  
  
 A tabela a seguir descreve cada nível de log disponível para as categorias de log internas.  
  
|Nome|Description|  
|----------|-----------------|  
|SEVERE|Indica uma falha séria e é o nível mais alto de log. No driver JDBC, este nível é usado para relatar erros e exceções.|  
|WARNING|Indica um problema potencial.|  
|INFO|Fornece mensagens informativas.|  
|FINE|Fornece informações de rastreamento que incluem criação e destruição básicas de objeto. Além disso, todas as exceções lançadas pelos métodos públicos.|  
|FINER|Fornece informações de rastreamento detalhadas inclusive todas as entradas de método público e pontos de saída com tipos de dados de parâmetro associados e todas as propriedades públicas para classes públicas. Além disso, parâmetro de entrada, parâmetros de saída e valores de retorno de método exceto CLOB, BLOB, NCLOB, Reader, \<fluxo > tipos de valor de retorno.<br /><br /> As seguintes categorias de log existiam na versão 1.2 do driver JDBC e tinham o nível de log FINE: [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), XA e [SQLServerDataSource ](../../connect/jdbc/reference/sqlserverdatasource-class.md). Desde a versão 2.0, estes são atualizados para o nível FINER.|  
|FINEST|Fornece informações de rastreamento altamente detalhadas. Este é o nível mais baixo de log.<br /><br /> As categorias de log a seguir existiam na versão 1.2 do driver JDBC e tinham o nível de log FINEST: TDS.DATA e TDS.TOKEN. Desde a versão 2.0, eles mantêm o nível de log FINEST.|  
|OFF|Desliga o log.|  
|ALL|Habilita log de todas as mensagens.|  
  
## <a name="logging-categories"></a>Categorias de log  
 Quando você cria um objeto de agente de log, você deve dizer a qual entidade ou categoria nomeada que você esteja interessado em obter informações de log. O driver JDBC suporta as categorias de log públicas a seguir, que estão todas definidas no pacote do driver com.microsoft.sqlserver.jdbc.  
  
|Nome|Description|  
|----------|-----------------|  
|Conexão|Registra mensagens no [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. Os aplicativos podem definir o nível de log como FINER.|  
|de|Registra mensagens no [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe. Os aplicativos podem definir o nível de log como FINER.|  
|DataSource|Registra mensagens no [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|ResultSet|Registra mensagens no [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe. Os aplicativos podem definir o nível de log como FINER.|  
|Driver|Registra mensagens no [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) classe. Os aplicativos podem definir o nível de log como FINER.|  
  
 A partir do Microsoft JDBC Driver versão 2.0, o driver também fornece o pacote com.microsoft.sqlserver.jdbc.internals, que inclui o suporte de log para as categorias de log internas a seguir.  
  
|Nome|Description|  
|----------|-----------------|  
|AuthenticationJNI|Problemas de autenticação integrada do registra mensagens sobre o Windows (quando o **authenticationScheme** propriedade de conexão é implicitamente ou explicitamente definida como **NativeAuthentication**).<br /><br /> Os aplicativos podem definir o nível de log como FINEST e FINE.|  
|SQLServerConnection|Registra mensagens no [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. Os aplicativos podem definir o nível de log como FINE e FINER.|  
|SQLServerDataSource|Registra mensagens no [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), e [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md) classes.<br /><br /> Os aplicativos podem definir o nível de log como FINER.|  
|InputStream|Registra mensagens relativas aos seguintes tipos de dados: java.io.InputStream, java.io.Reader e os tipos de dados que têm um especificador max como tipos de dados varchar, nvarchar e varbinary.<br /><br /> Os aplicativos podem definir o nível de log como FINER.|  
|SQLServerException|Registra mensagens no [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerResultSet|Registra mensagens no [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe. Os aplicativos podem definir o nível de log como FINE, FINER e FINEST.|  
|SQLServerStatement|Registra mensagens no [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe. Os aplicativos podem definir o nível de log como FINE, FINER e FINEST.|  
|XA|Registra mensagens para todas as transações XA a [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) classe. Os aplicativos podem definir o nível de log como FINE e FINER.|  
|KerbAuthentication|Registra mensagens sobre a autenticação Kerberos tipo 4 (quando o **authenticationScheme** conexão está definida como **JavaKerberos**). O aplicativo pode definir o nível de log como FINE ou FINER.|  
|TDS.DATA|Registra mensagens que contêm a conversa no nível do protocolo TDS entre o driver e o SQL Server. O conteúdo detalhado de cada pacote TDS enviado e recebido é registrado em ASCII e hexadecimal. As credenciais de logon (nomes de usuários e senhas) não são registradas. Todos os outros dados são registrados.<br /><br /> Esta categoria cria mensagens muito detalhadas e detalhadas, e só poderá ser habilitada definindo o nível de registro como FINEST.|  
|TDS.Channel|Esta categoria rastreia ações do canal de comunicação TCP com SQL Server. As mensagens registradas incluem abertura e fechamento de soquete, além de leituras e gravações. Elas também rastreiam mensagens relacionadas a estabelecer uma conexão de Protocolo SSL (SSL) com SQL Server.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINE, FINER ou FINEST.|  
|TDS.Writer|Esta categoria rastreia gravações no canal de TDS. Observe que somente o comprimento das gravações é rastreado, não o conteúdo. Esta categoria também rastreia problemas quando um sinal de atenção é enviado ao servidor para cancelar a execução de uma instrução.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINEST.|  
|TDS.Reader|Esta categoria rastreia determinadas operações de leitura do canal de TDS no nível FINEST. No nível FINEST, o rastreamento pode ser bastante detalhado. Nos níveis WARNING e SEVERE, esta categoria rastreia quando o driver recebe um protocolo TDS inválido do SQL Server antes de o driver fechar a conexão.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINER e FINEST.|  
|TDS.Command|Esta categoria rastreia transições de estado de baixo nível e outras informações associadas à execução de comandos TDS, como [!INCLUDE[tsql](../../includes/tsql_md.md)] execuções de instrução, buscas do cursor ResultSet, confirmações e assim por diante.<br /><br /> Esta categoria só poderá ser habilitada definindo o nível de log como FINEST.|  
|TDS.TOKEN|Esta categoria registra somente os tokens dentro dos pacotes TDS e é menos detalhada que a categoria TDS.DATA. Ela só poderá ser habilitada definindo o nível de log como FINEST.<br /><br /> No nível FINEST, esta categoria rastreia tokens de TDS à medida que eles são processados na resposta. No nível SEVERE, esta categoria rastreia quando um token de TDS inválido é encontrado.|  
|SQLServerDatabaseMetaData|Registra mensagens no [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerResultSetMetaData|Registra mensagens no [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerParameterMetaData|Registra mensagens no [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerBlob|Registra mensagens no [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerClob|Registra mensagens no [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerSQLXML|Registra mensagens na classe SQLServerSQLXML interna. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerDriver|Registra mensagens no [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
|SQLServerNClob|Registra mensagens no [SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md) classe. Os aplicativos podem definir o nível de log como FINE.|  
  
## <a name="enabling-tracing-programmatically"></a>Habilitando o rastreamento programaticamente  
 O rastreamento pode ser habilitado programaticamente criando um objeto de agente de log e indicando a categoria a ser registrada. Por exemplo, o código a seguir mostra como habilitar log para instruções SQL:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 Para desabilitar log no seu código, use o seguinte:  
  
```  
logger.setLevel(Level.OFF);  
```  
  
 Para registrar todas as categorias disponíveis, use o seguinte:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 Para desabilitar uma categoria específica de ser registrada, use o seguinte:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>Habilitando rastreamento usando o arquivo Logging.Properties  
 Você também pode habilitar rastreamento usando o `logging.properties` arquivo, que pode ser encontrado na `lib` diretório de instalação do Java Runtime Environment (JRE). Este arquivo poderá ser usado para definir os valores padrão para agentes e manipuladores que serão usados quando o rastreamento for habilitado.  
  
 A seguir está um exemplo das configurações que você pode fazer no `logging.properties` arquivos:  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  Você pode definir as propriedades `logging.properties` arquivo usando o objeto LogManager que faz parte do Logging.  
  
## <a name="see-also"></a>Consulte também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  

