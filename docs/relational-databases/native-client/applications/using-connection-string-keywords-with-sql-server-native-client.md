---
title: Usando palavras-chave de cadeia de caracteres de Conexão com o SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a322349b1916423347c26089e9b3898d026d338
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256331"
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>Usando palavras-chave da cadeia de conexão com o SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Algumas APIs do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usam cadeias de conexão para especificar atributos de conexão. Cadeias de conexão são listas de palavras-chave e valores associados; cada palavra-chave identifica um atributo de conexão específico.  
  
> **OBSERVAÇÃO:** O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client permite ambiguidade em cadeias de conexão a fim de manter a compatibilidade com versões anteriores (por exemplo, algumas palavras-chave podem ser especificadas mais de uma vez e outras, conflitantes, permitidas tendo a resolução baseada na posição ou na precedência). Futuras versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client talvez não permitam ambiguidade em cadeias de conexão. Trata-se de uma boa prática, ao modificar aplicativos, usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para eliminar todas as dependências relacionadas à ambiguidade da cadeia de conexão.  
  
 As seguintes seções descrevem as palavras-chave que podem ser usadas com o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o ADO (ActiveX Data Objects) durante o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como provedor de dados.  
  
## <a name="odbc-driver-connection-string-keywords"></a>Palavras-chave cadeia de caracteres de conexão do Driver ODBC  
 Aplicativos ODBC usam cadeias de caracteres de conexão como parâmetros para o [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) e [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) funções.  
  
 As cadeias de conexão usadas pelo ODBC têm a seguinte sintaxe:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Os valores de atributo podem ser colocados entre chaves, sendo uma boa prática fazer isso. Isso evita problemas quando os valores de atributo contêm caracteres não alfanuméricos. Como a primeira chave de fechamento é usada para encerrar o valor, os valores não podem conter caracteres de chave de fechamento.  
  
 A seguinte tabela descreve as palavras-chave que podem ser usadas com uma cadeia de conexão ODBC.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|**Addr**|Sinônimo de "Endereço".|  
|**Endereço**|O endereço de rede do servidor executando uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **Address** é normalmente o nome da rede do servidor, mas pode ter outros nomes como, um pipe, um endereço IP ou uma porta TCP/IP e endereço de soquete.<br /><br /> Se você especificar um endereço IP, verifique se os protocolos de pipes nomeados ou TCP/IP estão habilitados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> O valor de **endereço** prevalece sobre o valor passado para **Server** em cadeias de conexão ODBC ao usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Observe também que `Address=;` conecta-se com o servidor especificado na palavra-chave **Server**, enquanto que `Address= ;, Address=.;`, `Address=localhost;` e `Address=(local);` estabelecem uma conexão com o servidor local.<br /><br /> A sintaxe completa para a palavra-chave **Address** é a seguinte:<br /><br /> [_protocolo_**:**]*endereço*[**,**_porta &#124;\pipe\pipename_]<br /><br /> O*protocolo* pode ser **tcp** (TCP/IP), **lpc** (memória compartilhada) ou **np** (pipes nomeados). Para obter mais informações sobre os protocolos, consulte [configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Se nem *protocolo* nem a **rede** palavra-chave for especificado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usará a ordem de protocolo especificada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager.<br /><br /> *port* é a porta à qual se conectar, no servidor especificado. Por padrão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a porta 1433.|  
|**AnsiNPW**|No caso de "sim", o driver usa comportamentos definidos por ANSI para tratar comparações NULL, preenchimento de dados de caractere, avisos e concatenação NULL. Em caso de "não", os comportamentos definidos por ANSI não são expostos. Para obter mais informações sobre comportamentos NPW ANSI, consulte [efeitos das opções ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**APP**|Nome do aplicativo que chama [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) (opcional). Se for especificado, esse valor é armazenado na **Master** coluna **program_name** e é retornado pela [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) e o [APP_NAME](../../../t-sql/functions/app-name-transact-sql.md)funções.|  
|**ApplicationIntent**|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**. O padrão é **ReadWrite**.  Por exemplo:<br /><br /> `ApplicationIntent=ReadOnly`<br /><br /> Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte do cliente nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native Client dá suporte para alta disponibilidade, recuperação de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|Nome do arquivo primário de um banco de dados anexável. Inclua o caminho completo e remova todos os caracteres \ caso esteja usando uma variável da cadeia de caracteres C:<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> Esse banco de dados é anexado e torna-se o banco de dados padrão da conexão. Para usar **AttachDBFileName** você também deve especificar o nome do banco de dados em qualquer um os [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) parâmetro de banco de dados ou o atributo de conexão SQL_COPT_CURRENT_CATALOG. Caso o banco de dados já tenha sido anexado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não o anexa novamente; ele usa o banco de dados anexado como sendo o padrão da conexão.|  
|**AutoTranslate**|Em caso de "sim, as cadeias de caracteres ANSI enviadas entre o cliente e o servidor são traduzidas com a conversão por Unicode para minimizar problemas na correspondência de caracteres estendidos entre as páginas de código no cliente e no servidor.<br /><br /> Dados SQL_C_CHAR do cliente enviados para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, ou **texto** variável, parâmetro ou coluna é convertida de caractere em Unicode usando o cliente Página de código ANSI (ACP), em seguida, convertidos de Unicode em caractere usando a ACP do servidor.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, ou **texto** dados enviados para uma variável SQL_C_CHAR do cliente é convertidos de caractere em Unicode usando a ACP do servidor, em seguida, convertidos de Unicode em caractere usando o cliente ACP.<br /><br /> As conversões são executadas no cliente pelo driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Isso exige que a mesma ACP usada no servidor esteja disponível no cliente.<br /><br /> Estas configurações não têm nenhum efeito nas conversões que ocorrem para estas transferências:<br /><br /> \* Dados de cliente SQL_C_WCHAR de Unicode enviados para **char**, **varchar**, ou **texto** no servidor.<br /><br /> &#42;**char**, **varchar**, ou **texto** enviados a uma variável SQL_C_WCHAR de Unicode no cliente de dados do servidor.<br /><br /> \* Dados de cliente do SQL_C_CHAR de ANSI enviados para Unicode **nchar**, **nvarchar**, ou **ntext** no servidor.<br /><br /> \* Unicode **nchar**, **nvarchar**, ou **ntext** enviados a uma variável SQL_C_CHAR de ANSI no cliente de dados do servidor.<br /><br /> Em caso de "não", a conversão de caracteres não é realizada.<br /><br /> O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client não converte dados de SQL_C_CHAR do cliente ANSI caracteres enviados ao **char**, **varchar**, ou **texto** variáveis, parâmetros, ou colunas no servidor. Nenhuma conversão é executada nos **char**, **varchar**, ou **texto** dados enviados do servidor para as variáveis SQL_C_CHAR no cliente.<br /><br /> Caso o cliente e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estejam usando ACPs diferentes, os caracteres estendidos podem ser mal-interpretados.|  
|**Backup de banco de dados**|Nome do banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] padrão da conexão. Se **banco de dados** não for especificado, o banco de dados padrão definido para o logon é usado. O banco de dados padrão da fonte de dados ODBC substitui o banco de dados padrão definido para o logon. O banco de dados deve ser um banco de dados existente, a menos que **AttachDBFileName** também for especificado. Se **AttachDBFileName** também for especificado, o arquivo primário, ele aponta é anexado e recebe o nome do banco de dados especificado por **banco de dados**.|  
|**Driver**|Nome do driver como retornado por [SQLDrivers](../../../relational-databases/native-client-odbc-api/sqldrivers.md). O valor de palavra-chave do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é" {SQL Server Native Client 11.0}". O **Server** palavra-chave será necessária se **Driver** é especificado e **DriverCompletion** é definido como SQL_DRIVER_NOPROMPT.<br /><br /> Para obter mais informações sobre nomes de driver, consulte [usando os arquivos de biblioteca e cabeçalho do SQL Server Native Client](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md).|  
|**DSN**|Nome de um usuário de ODBC existente ou fonte de dados do sistema. Essa palavra-chave substitui qualquer valor que pode ser especificado na **Server**, **rede**, e **endereço** palavras-chave.|  
|**Encrypt**|Especifica se os dados devem ser criptografados antes de serem enviados pela rede. Os valores possíveis são "sim" e "não". O valor padrão é "não".|  
|**Fallback**|A palavra-chave é preterida e a configuração, ignorada pelo driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**Failover_Partner**|Nome do servidor de parceiro de failover a ser usado caso não seja possível estabelecer uma conexão com o servidor primário.|  
|**FailoverPartnerSPN**|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo driver.|  
|**FileDSN**|Nome de uma fonte de dados do arquivo ODBC existente.|  
|**Idioma**|Nome do idioma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (opcional). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode armazenar mensagens em vários idiomas no **sysmessages**. Se estiver se conectando a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com vários idiomas, **linguagem** Especifica qual conjunto de mensagens são usadas para a conexão.|  
|**MARS_Connection**|Habilita ou desabilita MARS (Multiple Active Result Sets) na conexão. Os valores reconhecidos são "sim" e "não". O padrão é "não".|  
|**MultiSubnetFailover**|Sempre especifique **multiSubnetFailover = Yes** ao se conectar ao ouvinte do grupo de disponibilidade de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grupo de disponibilidade ou um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de Cluster de Failover. **multiSubnetFailover = Yes** configura [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para fornecer detecção mais rápida e conexão para o servidor ativo (atualmente). Os valores possíveis são **Sim** e **Não**. O padrão é **No**. Por exemplo:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte do cliente nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native Client dá suporte para alta disponibilidade, recuperação de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Net**|Sinônimo de "Rede".|  
|**Rede**|Os valores válidos são **dbnmpntw** (pipes nomeados) e **dbmssocn** (TCP/IP).<br /><br /> É um erro para especificar um valor para o **rede** palavra-chave e um protocolo de prefixo na **Server** palavra-chave.|  
|**PWD**|A senha para a conta de login para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificada no parâmetro UID. **PWD** não precisa ser especificado se o logon tiver uma senha NULL ou ao usar a autenticação do Windows (`Trusted_Connection = yes`).|  
|**QueryLog_On**|Em caso de "sim", o registro em log de dados de consultas demoradas é habilitado na conexão. Em caso de "não", os dados de consultas demoradas não são registrados.|  
|**QueryLogFile**|Caminho completo e nome de um arquivo a ser usado para registrar em log dados de consultas demoradas.|  
|**QueryLogTime**|Cadeia de caracteres de dígito que especifica o limite (em milissegundos) para registrar em log consultas demoradas. Qualquer consulta que não receba uma resposta na hora especificada é gravada no arquivo de log de consultas demoradas.|  
|**QuotedId**|Em caso de "sim", QUOTED_IDENTIFIERS é definido como ON para a conexão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa as regras de ISO referentes ao uso de aspas em instruções SQL. Quando não, QUOTED_IDENTIFIERS será definido como OFF para a conexão. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] segue as regras de [!INCLUDE[tsql](../../../includes/tsql-md.md)] herdadas em relação ao uso de aspas em instruções SQL. Para obter mais informações, consulte [efeitos das opções ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**Regional**|Em caso de "sim", o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usa configurações do cliente ao converter dados de moeda, data e hora em dados de caractere. A conversão é apenas um meio; o driver não reconhece formatos padrão que não sejam ODBC para cadeias de caracteres de data ou valores de moeda contidos. Por exemplo, um parâmetro usado em uma instrução INSERT ou UPDATE. Em caso de "não", o driver usa as cadeias de caracteres padrão ODBC para representar dados de moeda, data e hora convertidos em dados de caractere.|  
|**SaveFile**|Nome de um arquivo de fonte de dados ODBC no qual os atributos da conexão atual serão salvos em caso de êxito na conexão.|  
|**Servidor**|O nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O valor deve ser o nome de um servidor na rede, um endereço IP ou o nome de um alias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> O **endereço** palavra-chave substitui o **Server** palavra-chave.<br /><br /> É possível se conectar à instância padrão no servidor local especificando uma das seguintes opções:<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** _instancename_ **;**<br /><br /> Para obter mais informações sobre suporte ao LocalDB, consulte [SQL Server Native Client dá suporte para LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md).<br /><br /> Para especificar uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], acrescente **\\** _InstanceName_.<br /><br /> Quando nenhum servidor está especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> Se você especificar um endereço IP, verifique se os protocolos de pipes nomeados ou TCP/IP estão habilitados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> A sintaxe completa para a palavra-chave **Server** é a seguinte:<br /><br /> **Server=**[_protocol_**:**]*Server*[**,**_port_]<br /><br /> O*protocolo* pode ser **tcp** (TCP/IP), **lpc** (memória compartilhada) ou **np** (pipes nomeados).<br /><br /> O seguinte é um exemplo de como especificar um pipe nomeado:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Esta linha especifica o protocolo de pipe nomeado, um pipe nomeado na máquina local (`\\.\pipe`), o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) e o nome padrão do pipe nomeado (`sql/query`).<br /><br /> Se nem um *protocolo* nem a **rede** palavra-chave for especificado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usará a ordem de protocolo especificada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager.<br /><br /> *port* é a porta à qual se conectar, no servidor especificado. Por padrão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a porta 1433.<br /><br /> Os espaços são ignorados no início do valor passado para **Server** nas cadeias de conexão ODBC ao usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**ServerSPN**|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo driver.|  
|**StatsLog_On**|Em caso de "sim", habilita a captura dos dados de desempenho do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Em caso de "não", os dados de desempenho do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não permanecem disponíveis na conexão.|  
|**StatsLogFile**|Caminho completo e nome de um arquivo usado para registrar estatísticas de desempenho do driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**Trusted_Connection**|Em caso de "sim", instrui o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a usar o modo de Autenticação do Windows na validação do logon. Do contrário, instrui o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a usar um nome de usuário e uma senha do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na validação do logon, e as palavras-chave UID e PWD devem ser especificadas.|  
|**TrustServerCertificate**|Quando usado com **Encrypt**, habilita a criptografia usando um certificado de servidor autoassinado.|  
|**UID**|Uma conta de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válida. O UID não precisa ser especificado durante o uso da Autenticação do Windows.|  
|**UseProcForPrepare**|Essa palavra-chave é preterida e a configuração, ignorada pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Driver de ODBC do Native Client.|  
|**WSID**|A ID da estação de trabalho. Normalmente, trata-se do nome de rede do computador em que está o aplicativo (opcional). Se for especificado, esse valor é armazenado na **Master** coluna **nome do host** e é retornado pela [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) e o [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)função.|  
  
> **OBSERVAÇÃO:** As configurações regionais de conversão se aplicam a tipos de dados de moeda, numéricos e de data e hora. A configuração da conversão só se aplica à conversão de saída, sendo visível apenas quando valores de moeda, número, data ou hora são convertidos em cadeias de caracteres.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usa as configurações do Registro de localidade do usuário atual. O driver não honra a localidade do thread atual se o aplicativo defina após a conexão, por exemplo, chamar **SetThreadLocale**.  
  
 A alteração do comportamento regional de uma fonte de dados pode fazer o aplicativo falhar. Um aplicativo que analisa cadeias de caracteres de data e espera que elas sejam exibidas conforme definição do ODBC poderia ser afetado negativamente pela alteração desse valor.  
  
## <a name="ole-db-provider-connection-string-keywords"></a>Palavras-chave da cadeia de conexão do provedor OLE DB  
 Os aplicativos OLE DB podem inicializar objetos de fonte de dados de duas formas:  
  
-   **IDBInitialize::Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 No primeiro caso, uma cadeia de caracteres do provedor pode ser usada para inicializar as propriedades da conexão, definindo a propriedade DBPROP_INIT_PROVIDERSTRING no conjunto de propriedades DBPROPSET_DBINIT. No segundo, uma cadeia de caracteres de inicialização pode ser passada para o método **IDataInitialize::GetDataSource** a fim de inicializar as propriedades da conexão. Ambos os métodos inicializam as mesmas propriedades de conexão OLE DB, embora sejam usados conjuntos diferentes de palavras-chave. O conjunto de palavras-chave usado por **IDataInitialize::GetDataSource** é, no mínimo, a descrição das propriedades dentro do grupo de propriedades de inicialização.  
  
 Qualquer configuração da cadeia de caracteres do provedor tem uma propriedade OLE DB correspondente definida com um valor padrão ou explicitamente definida com um valor; o valor de propriedade OLE DB substituirá a configuração na cadeia de caracteres do provedor.  
  
 As propriedades boolianas definidas nas cadeias de caracteres do provedor por meio dos valores DBPROP_INIT_PROVIDERSTRING são definidas usando os valores "sim" e "não". As propriedades boolianas definidas nas cadeias de caracteres de inicialização que usam **IDataInitialize::GetDataSource** são definidas usando os valores "verdadeiro" e "falso".  
  
 Os aplicativos que usam **IDataInitialize::GetDataSource** também podem usar as palavras-chave usadas por **IDBInitialize::Initialize**, mas só para propriedades que não tenham um valor padrão. Caso um aplicativo use ambas as palavras-chave **IDataInitialize::GetDataSource** e **IDBInitialize::Initialize** na cadeia de caracteres de inicialização, é usada a definição da palavra-chave **IDataInitialize::GetDataSource**. É altamente recomendável que os aplicativos não usem palavras-chave **IDBInitialize::Initialize** em cadeias de conexão **IDataInitialize:GetDataSource**, uma vez que esse comportamento talvez não seja mantido em versões futuras.  
  
> [!NOTE]  
>  Uma cadeia de conexão passada por meio de **IDataInitialize::GetDataSource** é convertida em propriedades e aplicada por meio de **IDBProperties::SetProperties**. Se os serviços de componente encontraram a descrição da propriedade em **IDBProperties::GetPropertyInfo**, essa propriedade será aplicada como uma propriedade autônoma. Caso contrário, ela será aplicada por meio da propriedade DBPROP_PROVIDERSTRING. Por exemplo, se você especificar a cadeia de caracteres de conexão **fonte de dados = server1; Server = server2**, **fonte de dados** será definido como uma propriedade, mas **servidor** entrará em uma cadeia de caracteres do provedor.  
  
 Se você especificar várias instâncias da mesma propriedade específica do provedor, o primeiro valor da primeira propriedade será usado.  
  
 As cadeias de conexão usadas por aplicativos OLE DB que usam DBPROP_INIT_PROVIDERSTRING com **IDBInitialize::Initialize** têm a seguinte sintaxe:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Os valores de atributo podem ser colocados entre chaves, sendo uma boa prática fazer isso. Isso evita problemas quando os valores de atributo contêm caracteres não alfanuméricos. Como a primeira chave de fechamento é usada para encerrar o valor, os valores não podem conter caracteres de chave de fechamento.  
  
 Um caractere de espaço após o sinal de igual (=) de uma palavra-chave de cadeia de conexão será interpretado como um literal, mesmo que o valor seja colocado entre aspas.  
  
 A tabela a seguir descreve as palavras-chave que podem ser usadas com DBPROP_INIT_PROVIDERSTRING.  
  
|Palavra-chave|Propriedade de inicialização|Descrição|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|Sinônimo de "Endereço".|  
|**Endereço**|SSPROP_INIT_NETWORKADDRESS|O endereço de rede de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Para obter mais informações sobre a sintaxe de endereço válida, consulte a descrição do **endereço** palavra-chave ODBC, neste tópico.|  
|**APP**|SSPROP_INIT_APPNAME|A cadeia de caracteres que identifica o aplicativo.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.<br /><br /> O padrão é **ReadWrite**. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte do cliente nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native Client dá suporte para alta disponibilidade, recuperação de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|O nome do arquivo primário (com o nome do caminho completo incluído) de um banco de dados anexável. Para usar **AttachDBFileName**, você também deve especificar o nome do banco de dados com a palavra-chave Database da cadeia de caracteres do provedor. Caso o banco de dados já tenha sido anexado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não o anexa novamente (ele usa o banco de dados anexado como sendo o padrão da conexão).|  
|**Tradução automática**|SSPROP_INIT_AUTOTRANSLATE|Sinônimo de "Tradução automática".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura a conversão de caracteres OEM/ANSI. Os valores reconhecidos são "sim" e "não".|  
|**Backup de banco de dados**|DBPROP_INIT_CATALOG|Nome do banco de dados.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica o modo de manipulação do tipo de dados a ser usado. Os valores reconhecidos são "0" para tipos de dados do provedor e "80" para tipos de dados do SQL Server 2000.|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|Especifica se os dados devem ser criptografados antes de serem enviados pela rede. Os valores possíveis são "sim" e "não". O valor padrão é "não".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|O nome do servidor de failover usado no espelhamento de banco de dados.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo provedor.|  
|**Idioma**|SSPROPT_INIT_CURRENTLANGUAGE|O idioma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Habilita ou desabilita MARS na conexão caso o servidor seja [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior. Os valores possíveis são "sim" e "não". O valor padrão é "não".|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|Sinônimo de "Rede".|  
|**Rede**|SSPROP_INIT_NETWORKLIBRARY|A biblioteca de rede usada para estabelecer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.|  
|**Biblioteca de rede**|SSPROP_INIT_NETWORKLIBRARY|Sinônimo de "Rede".|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|Tamanho do pacote de rede. O padrão é 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Aceita as cadeias de caracteres "sim" e "não" como valores. Em caso de "não", o objeto de fonte de dados não tem permissão para manter informações confidenciais de autenticação|  
|**PWD**|DBPROP_AUTH_PASSWORD|A senha de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Servidor**|DBPROP_INIT_DATASOURCE|O nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Quando não especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> Para obter mais informações sobre a sintaxe de endereço válida, consulte a descrição do **Server** palavra-chave ODBC, neste tópico.|  
|**ServerSPN**|SSPROP_INIT_SERVERSPN|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo provedor.|  
|**Tempo Limite**|DBPROP_INIT_TIMEOUT|O tempo (em segundos) para aguardar a conclusão da inicialização da fonte de dados.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Em caso de "sim", instrui o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a usar o modo de Autenticação do Windows na validação do logon. Do contrário, instrui o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a usar um nome de usuário e uma senha do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na validação do logon, e as palavras-chave UID e PWD devem ser especificadas.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Aceita as cadeias de caracteres "sim" e "não" como valores. O valor padrão é "não", o que significa que o certificado do servidor será validado.|  
|**UID**|DBPROP_AUTH_USERID|O nome de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|A palavra-chave é preterida e a configuração, ignorada pelo provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**WSID**|SSPROP_INIT_WSID|O identificador da estação de trabalho.|  
  
 As cadeias de conexão usadas por aplicativos OLE DB que usam **IDataInitialize::GetDataSource** têm a seguinte sintaxe:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 O uso de propriedades deve estar em conformidade com a sintaxe permitida em seu escopo.  Por exemplo, **WSID** usa caracteres de chaves (**{}**) e **Application Name** usa caracteres de aspas simples (**'**) ou de aspas duplas (**"**). Apenas propriedades de cadeia de caracteres podem ser colocadas entre aspas. A tentativa de colocar um número inteiro ou propriedade enumerada entre aspas resultará no erro: "A Cadeia de Conexão não está de acordo com a especificação OLE DB".  
  
 Opcionalmente, os valores de atributos podem ser colocados entre aspas simples ou duplas, o que é uma boa prática. Isso evita problemas quando os valores contêm caracteres não alfanuméricos. O caractere de aspas usado também pode ser exibido em valores, desde que seja dobrado.  
  
 Um caractere de espaço após o sinal de igual (=) de uma palavra-chave de cadeia de conexão será interpretado como um literal, mesmo que o valor seja colocado entre aspas.  
  
 Se uma cadeia de conexão tiver mais de uma das propriedades listadas na tabela a seguir, o valor da última propriedade será usado.  
  
 A tabela a seguir descreve as palavras-chave que podem ser usadas com **IDataInitialize::GetDataSource**:  
  
|Palavra-chave|Propriedade de inicialização|Descrição|  
|-------------|-----------------------------|-----------------|  
|**Nome do Aplicativo**|SSPROP_INIT_APPNAME|A cadeia de caracteres que identifica o aplicativo.|  
|**Intenção do aplicativo**|SSPROP_INIT_APPLICATIONINTENT|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.<br /><br /> O padrão é **ReadWrite**. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte do cliente nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native Client dá suporte para alta disponibilidade, recuperação de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Tradução automática**|SSPROP_INIT_AUTOTRANSLATE|Sinônimo de "Tradução automática".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura a conversão de caracteres OEM/ANSI. Os valores reconhecidos são "verdadeiro" e "falso".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|O tempo (em segundos) para aguardar a conclusão da inicialização da fonte de dados.|  
|**Idioma Atual**|SSPROPT_INIT_CURRENTLANGUAGE|O nome do idioma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Fonte de dados**|DBPROP_INIT_DATASOURCE|O nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Quando não especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> Para obter mais informações sobre a sintaxe de endereço válida, consulte a descrição do **Server** palavra-chave ODBC, neste tópico.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica o modo de manipulação do tipo de dados a ser usado. Os valores reconhecidos são "0" para tipos de dados de provedor e "80" para tipos de dados do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|O nome do servidor de failover usado no espelhamento de banco de dados.|  
|**SPN do parceiro de failover**|SSPROP_INIT_FAILOVERPARTNERSPN|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo provedor.|  
|**Catálogo Inicial**|DBPROP_INIT_CATALOG|Nome do banco de dados.|  
|**Nome do arquivo**|SSPROP_INIT_FILENAME|O nome do arquivo primário (com o nome do caminho completo incluído) de um banco de dados anexável. Para usar **AttachDBFileName**, você também deve especificar o nome do banco de dados com a palavra-chave DATABASE da cadeia de caracteres do provedor. Caso o banco de dados já tenha sido anexado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não o anexa novamente (ele usa o banco de dados anexado como sendo o padrão da conexão).|  
|**Segurança Integrada**|DBPROP_AUTH_INTEGRATED|Aceita o valor o "SSPI" para a Autenticação do Windows.|  
|**Conexão MARS**|SSPROP_INIT_MARSCONNECTION|Habilita ou desabilita MARS (Multiple Active Result Sets) na conexão. Os valores reconhecidos são "verdadeiro" e "falso". O padrão é "falso".|  
|**Endereço de rede**|SSPROP_INIT_NETWORKADDRESS|O endereço de rede de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Para obter mais informações sobre a sintaxe de endereço válida, consulte a descrição do **endereço** palavra-chave ODBC, neste tópico.|  
|**Biblioteca de rede**|SSPROP_INIT_NETWORKLIBRARY|A biblioteca de rede usada para estabelecer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamanho do pacote de rede. O padrão é 4096.|  
|**Senha**|DBPROP_AUTH_PASSWORD|A senha de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. Em caso de "falso", o objeto de fonte de dados não tem permissão para manter informações confidenciais de autenticação|  
|**Provedor**||No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, isso deve ser "SQLNCLI11".|  
|**SPN do servidor**|SSPROP_INIT_SERVERSPN|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo provedor.|  
|**Confiar em Certificado do Servidor**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. O valor padrão é "falso", o que significa que o certificado do servidor será validado.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Especifica se os dados devem ser criptografados antes de serem enviados pela rede. Os valores possíveis são "verdadeiro" e "falso". O valor padrão é "falso".|  
|**ID de usuário**|DBPROP_AUTH_USERID|O nome de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**ID da estação de trabalho**|SSPROP_INIT_WSID|O identificador da estação de trabalho.|  
  
 **Observação** Na cadeia de conexão, a propriedade "Old Password" define SSPROP_AUTH_OLD_PASSWORD, que é a senha atual (provavelmente expirada) que não está disponível por meio de uma propriedade de cadeia de caracteres do provedor.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>Palavras-chave da cadeia de conexão do ADO (ActiveX Data Objects)  
 Os aplicativos ADO definem a propriedade **ConnectionString** dos objetos **ADODBConnection** ou fornecem uma cadeia de conexão como um parâmetro ao método **Open** de objetos **ADODBConnection**.  
  
 Os aplicativos ADO também podem usar as palavras-chave usadas pelo método **IDBInitialize::Initialize** do OLE DB, mas só para propriedades que não tenham um valor padrão. Se um aplicativo usar as palavras-chave do ADO e **IDBInitialize::Initialize** na cadeia de caracteres de inicialização, a configuração da palavra-chave do ADO será usada. É altamente recomendável que os aplicativos só usem palavras-chave da cadeia de conexão do ADO.  
  
 As cadeias de conexão usadas pelo ADO têm a seguinte sintaxe:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Os valores de atributo podem ser colocados entre aspas duplas, sendo uma boa prática fazer isso. Isso evita problemas quando os valores contêm caracteres não alfanuméricos. Os valores de atributo não podem conter aspas duplas.  
  
 A seguinte tabela descreve as palavras-chave que podem ser usadas com uma cadeia de conexão do ADO:  
  
|Palavra-chave|Propriedade de inicialização|Descrição|  
|-------------|-----------------------------|-----------------|  
|**Intenção do aplicativo**|SSPROP_INIT_APPLICATIONINTENT|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.<br /><br /> O padrão é **ReadWrite**. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte do cliente nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native Client dá suporte para alta disponibilidade, recuperação de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Nome do Aplicativo**|SSPROP_INIT_APPNAME|A cadeia de caracteres que identifica o aplicativo.|  
|**Tradução automática**|SSPROP_INIT_AUTOTRANSLATE|Sinônimo de "Tradução automática".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura a conversão de caracteres OEM/ANSI. Os valores reconhecidos são "verdadeiro" e "falso".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|O tempo (em segundos) para aguardar a conclusão da inicialização da fonte de dados.|  
|**Idioma Atual**|SSPROPT_INIT_CURRENTLANGUAGE|O nome do idioma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Fonte de dados**|DBPROP_INIT_DATASOURCE|O nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Quando não especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> Para obter mais informações sobre a sintaxe de endereço válida, consulte a descrição do **Server** palavra-chave ODBC, neste tópico.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica o modo de manuseio do tipo de dados a ser usado. Os valores reconhecidos são "0" para tipos de dados do provedor e "80" para tipos de dados do SQL Server 2000.|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|O nome do servidor de failover usado no espelhamento de banco de dados.|  
|**SPN do parceiro de failover**|SSPROP_INIT_FAILOVERPARTNERSPN|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo provedor.|  
|**Catálogo Inicial**|DBPROP_INIT_CATALOG|Nome do banco de dados.|  
|**Nome do arquivo**|SSPROP_INIT_FILENAME|O nome do arquivo primário (com o nome do caminho completo incluído) de um banco de dados anexável. Para usar **AttachDBFileName**, você também deve especificar o nome do banco de dados com a palavra-chave DATABASE da cadeia de caracteres do provedor. Caso o banco de dados já tenha sido anexado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não o anexa novamente (ele usa o banco de dados anexado como sendo o padrão da conexão).|  
|**Segurança Integrada**|DBPROP_AUTH_INTEGRATED|Aceita o valor o "SSPI" para a Autenticação do Windows.|  
|**Conexão MARS**|SSPROP_INIT_MARSCONNECTION|Habilita ou desabilita MARS na conexão caso o servidor seja [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior. Os valores reconhecidos são "verdadeiro" e "falso".O padrão é "falso".|  
|**Endereço de rede**|SSPROP_INIT_NETWORKADDRESS|O endereço de rede de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Para obter mais informações sobre a sintaxe de endereço válida, consulte a descrição do **endereço** palavra-chave ODBC, neste tópico.|  
|**Biblioteca de rede**|SSPROP_INIT_NETWORKLIBRARY|A biblioteca de rede usada para estabelecer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamanho do pacote de rede. O padrão é 4096.|  
|**Senha**|DBPROP_AUTH_PASSWORD|A senha de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. Quando "falso", o objeto de fonte de dados não tem permissão para manter informações confidenciais de autenticação.|  
|**Provedor**||No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, isso deve ser "SQLNCLI11".|  
|**SPN do servidor**|SSPROP_INIT_SERVERSPN|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client use o SPN padrão, gerado pelo provedor.|  
|**Confiar em Certificado do Servidor**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. O valor padrão é "falso", o que significa que o certificado do servidor será validado.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Especifica se os dados devem ser criptografados antes de serem enviados pela rede. Os valores possíveis são "verdadeiro" e "falso". O valor padrão é "falso".|  
|**ID de usuário**|DBPROP_AUTH_USERID|O nome de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**ID da estação de trabalho**|SSPROP_INIT_WSID|O identificador da estação de trabalho.|  
  
 **Observação** Na cadeia de conexão, a propriedade "Old Password" define SSPROP_AUTH_OLD_PASSWORD, que é a senha atual (provavelmente expirada) que não está disponível por meio de uma propriedade de cadeia de caracteres do provedor.  
  
## <a name="see-also"></a>Confira também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
