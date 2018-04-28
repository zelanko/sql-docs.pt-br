---
title: DSN e Conexão String palavras-chave e atributos usados no Driver ODBC para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: ''
ms.topic: article
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b5494a24e48b1d3e997079aba77682dddae7bda7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="dsn-and-connection-string-keywords-and-attributes"></a>DSN e palavras-chave de cadeia de caracteres de Conexão e atributos

Esta página lista as palavras-chave para as cadeias de conexão e DSNs e atributos de conexão para SQLSetConnectAttr e SQLGetConnectAttr, disponível no Driver ODBC para SQL Server.



## <a name="supported-dsnconnection-string-keywords-and-connection-attributes"></a>Palavras-chave de cadeia de caracteres de Conexão/DSN e atributos de Conexão com suporte

A tabela a seguir lista as palavras-chave disponíveis e os atributos para cada plataforma (l: Linux; M: Mac; W: Windows).
Clique na palavra-chave ou um atributo para obter mais detalhes.

| DSN / palavra-chave de cadeia de caracteres de Conexão | Atributo de Conexão | Plataforma | 
|-|-|-|
| [Endereço](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Endereço](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [AnsiNPW](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) |  [SQL_COPT_SS_ANSI_NPW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssansinpw) | LMW |
| [APP](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ApplicationIntent](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_APPLICATION_INTENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssapplicationintent) | LMW |
| [AttachDBFileName](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ATTACHDBFILENAME](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssattachdbfilename) | LMW |
| [Autenticação](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sqlcoptssauthentication) | [SQL_COPT_SS_AUTHENTICATION](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sqlcoptssauthentication) | LMW |
| [AutoTranslate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRANSLATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstranslate) | LMW |
| [ColumnEncryption](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sqlcoptsscolumnencryption) | [SQL_COPT_SS_COLUMN_ENCRYPTION](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sqlcoptsscolumnencryption) | LMW |
| [ConnectRetryCount](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_COUNT](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | L |
| [ConnectRetryInterval](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_INTERVAL](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | L |
| [Banco de dados](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_ATTR_CURRENT_CATALOG](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| [Descrição](../../connect/odbc/dsn-connection-string-attribute.md#description) | | LMW |
| [Driver](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [DSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Encrypt](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ENCRYPT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssencrypt) | LMW |
| [Failover_Partner](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssfailoverpartner) | L |
| [FailoverPartnerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | L |
| [FileDSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [KeystoreAuthentication](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystorePrincipalId](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystoreSecret](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [Idioma](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [MARS_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MARS_ENABLED](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmarsenabled) | LMW |
| [MultiSubnetFailover](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MULTISUBNET_FAILOVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmultisubnetfailover) | LMW |
| [NET](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Rede](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [PWD](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [QueryLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquery) | L |
| [QueryLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquerylog) | L |
| [QueryLogTIme](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_INTERVAL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfqueryinterval) | L |
| [QuotedId](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_QUOTED_IDENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssquotedident) | LMW |
| [Regional](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [SaveFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Servidor](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ServerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_SERVER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| [StatsLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdata) | L |
| [StatsLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalog) | L |
| [TransparentNetworkIPResolution](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sqlcoptsstnir) | [SQL_COPT_SS_TNIR](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sqlcoptsstnir) | LMW |
| [Trusted_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_INTEGRATED_SECURITY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssintegratedsecurity) | LMW |
| [TrustServerCertificate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRUST_SERVER_CERTIFICATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstrustservercertificate) | LMW |
| [UID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [UseFMTONLY](../../connect/odbc/dsn-connection-string-attribute.md#usefmtonly) | | LMW |
| [WSID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| | [SQL_ATTR_ACCESS_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ACCESS_MODE) | LMW |
| | [SQL_ATTR_ASYNC_DBC_EVENT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | L |
| | [SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | L |
| | [SQL_ATTR_ASYNC_DBC_PCALLBACK](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | L |
| | [SQL_ATTR_ASYNC_DBC_PCONTEXT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | L |
| | [SQL_ATTR_ASYNC_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | L |
| | [SQL_ATTR_AUTO_IPD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_AUTOCOMMIT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_AUTOCOMMIT) | LMW |
| | [SQL_ATTR_CONNECTION_DEAD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_CONNECTION_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_DBC_INFO_TOKEN](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_LOGIN_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_LOGIN_TIMEOUT) | LMW |
| | [SQL_ATTR_METADATA_ID](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_ODBC_CURSORS](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ODBC_CURSORS) | LMW |
| | [SQL_ATTR_PACKET_SIZE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_PACKET_SIZE) | LMW |
| | [SQL_ATTR_QUIET_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_QUIET_MODE) | LMW |
| | [SQL_ATTR_RESET_CONNECTION](../../odbc/reference/develop-driver/upgrading-a-3-5-driver-to-a-3-8-driver.md#connection-pooling) <br> (SQL_COPT_SS_RESET_CONNECTION) | LMW |  
| | [SQL_ATTR_TRACE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACE) | LMW |
| | [SQL_ATTR_TRACEFILE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACEFILE) | LMW |
| | [SQL_ATTR_TRANSLATE_LIB](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_DLL) | LMW |
| | [SQL_ATTR_TRANSLATE_OPTION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_OPTION) | LMW |
| | [SQL_ATTR_TXN_ISOLATION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TXN_ISOLATION) | LMW |
| | [SQL_COPT_SS_ACCESS_TOKEN](dsn-connection-string-attribute.md#sqlcoptssaccesstoken) | LMW |
| | [SQL_COPT_SS_ANSI_OEM](dsn-connection-string-attribute.md#sqlcoptssansioem)| L |
| | [SQL_COPT_SS_BCP](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbcp) | LMW |
| | [SQL_COPT_SS_BROWSE_CACHE_DATA](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) | LMW |
| | [SQL_COPT_SS_BROWSE_CONNECT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseconnect) | LMW |
| | [SQL_COPT_SS_BROWSE_SERVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseserver) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREDATA](dsn-connection-string-attribute.md#sqlcoptsscekeystoredata) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREPROVIDER](dsn-connection-string-attribute.md#sqlcoptsscekeystoreprovider) | LMW |
| | [SQL_COPT_SS_CLIENT_CONNECTION_ID](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md#sqlcoptssclientconnectionid) | LMW |
| | [SQL_COPT_SS_CONCAT_NULL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconcatnull) | LMW |
| | [SQL_COPT_SS_CONNECTION_DEAD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconnectiondead) | LMW |
| | [SQL_COPT_SS_ENLIST_IN_DTC](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistindtc) | L |
| | [SQL_COPT_SS_ENLIST_IN_XA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistinxa) | L |
| | [SQL_COPT_SS_FALLBACK_CONNECT](dsn-connection-string-attribute.md#sqlcoptssfallbackconnect) | LMW |
| | [SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_MUTUALLY_AUTHENTICATED](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_OLDPWD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssoldpwd) | LMW |
| | [SQL_COPT_SS_PERF_DATA_LOG_NOW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalognow) | L |
| | [SQL_COPT_SS_PRESERVE_CURSORS](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsspreservecursors) | LMW |
| | [SQL_COPT_SS_TXN_ISOLATION](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstxnisolation) | LMW |
| | [SQL_COPT_SS_USER_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssuserdata) | LMW |
| | [SQL_COPT_SS_WARN_ON_CP_ERROR](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsswarnoncperror) | LMW |


Aqui estão algumas palavras-chave de cadeia de caracteres de conexão e os atributos de conexão que não estão documentados no [usando Conexão String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md), [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [Função SQLSetConnectAttr](../../odbc/reference/syntax/sqlsetconnectattr-function.md).

### <a name="description"></a>Description

Usado para descrever a fonte de dados.

### <a name="sqlcoptssansioem"></a>SQL_COPT_SS_ANSI_OEM

Controles de ANSI para a conversão de dados de OEM. 

| Valor de atributo | Description |
|-|-|
| SQL_AO_OFF | (Padrão) Conversão não será executada. |
| SQL_AO_ON | Conversão é executada. |

### <a name="sqlcoptssfallbackconnect"></a>SQL_COPT_SS_FALLBACK_CONNECT

Controla o uso de conexões de Fallback do SQL Server. Este não é mais suportada.

| Valor de atributo | Description |
|-|-|
| SQL_FB_OFF | (Padrão) Conexões de fallback estão desabilitadas. |
| SQL_FB_ON | Conexões de fallback estão habilitados. |



## <a name="new-connection-string-keywords-and-connection-attributes"></a>Novas palavras-chave de cadeia de caracteres de Conexão e os atributos de Conexão

###  <a name="authentication---sqlcoptssauthentication"></a>Autenticação - SQL_COPT_SS_AUTHENTICATION

Define o modo de autenticação para usar ao se conectar ao SQL Server. Consulte [usando o Azure Active Directory](using-azure-active-directory.md) para obter mais informações.

| Valor de palavra-chave | Valor de atributo | Description |
|-|-|-|
| |SQL_AU_NONE|(Padrão) Não definido. Combinação de outros atributos determina o modo de autenticação.|
|SqlPassword|SQL_AU_PASSWORD|Autenticação do SQL Server com o nome de usuário e senha.|
|ActiveDirectoryIntegrated|SQL_AU_AD_INTEGRATED|Autenticação integrada do Active Directory do Azure.|
|ActiveDirectoryPassword|SQL_AU_AD_PASSWORD|Autenticação de senha do Active Directory do Azure.|
|ActiveDirectoryInteractive|SQL_AU_AD_INTERACTIVE|Autenticação interativa do Active Directory do Azure.|
| |SQL_AU_RESET|Não definida. Substitui qualquer DSN ou configuração de cadeia de caracteres de conexão.|

### <a name="columnencryption---sqlcoptsscolumnencryption"></a>ColumnEncryption - SQL_COPT_SS_COLUMN_ENCRYPTION

Controla a criptografia transparente de coluna (Always Encrypted). Consulte [usando criptografado sempre (ODBC)](using-always-encrypted-with-the-odbc-driver.md) para obter mais informações.

| Valor de palavra-chave | Valor de atributo | Description |
|-|-|-|
|Ativado|SQL_CE_ENABLED|Habilita o sempre criptografada.|
|Desabilitado|SQL_CE_DISABLED|(Padrão) Desabilita o sempre criptografada.|
| |SQL_CE_RESULTSETONLY|Permite descriptografia apenas (resultados e valores de retorno).|

### <a name="transparentnetworkipresolution---sqlcoptsstnir"></a>TransparentNetworkIPResolution - SQL_COPT_SS_TNIR

Controla o recurso de resolução de IP de rede transparente, que interage com MultiSubnetFailover para permitir uma reconexão mais rápida tentativas. Consulte [usando resolução de IP de rede transparente](using-transparent-network-ip-resolution.md) para obter mais informações.

| Valor de palavra-chave | Valor de atributo| Description |
|-|-|-|
|Sim|SQL_IS_ON|(Padrão) Permite a resolução IP de rede transparente.|
|não|SQL_IS_OFF|Desabilita a resolução IP de rede transparente.|

### <a name="usefmtonly"></a>UseFMTONLY

Controla o uso de SET FMTONLY para metadados ao conectar-se ao SQL Server 2012 e mais recente.

| Valor de palavra-chave | Description |
|-|-|
|não|(Padrão) Use sp_describe_first_result_set para metadados, se disponível. |
|Sim| Use SET FMTONLY para metadados. |

### <a name="sqlcoptssaccesstoken"></a>SQL_COPT_SS_ACCESS_TOKEN

Permite o uso de um token de acesso do Active Directory do Azure para autenticação. Consulte [usando o Azure Active Directory](using-azure-active-directory.md) para obter mais informações.

| Valor de atributo | Description |
|-|-|
| NULL | (Padrão) Nenhum token de acesso é fornecido. |
| ACCESSTOKEN * | Ponteiro para um token de acesso. |

### <a name="sqlcoptsscekeystoredata"></a>SQL_COPT_SS_CEKEYSTOREDATA

Se comunica com uma biblioteca de provedor de keystore carregado. Consulte a criptografia de coluna transparente de controles (Always Encrypted). Esse atributo não tem valor padrão. Consulte [provedores de armazenamento de chaves personalizado](custom-keystore-providers.md) para obter mais informações.

| Valor de atributo | Description |
|-|-|
| CEKEYSTOREDATA * | Estrutura de comunicação de dados para a biblioteca de provedor de armazenamento de chaves |

### <a name="sqlcoptsscekeystoreprovider"></a>SQL_COPT_SS_CEKEYSTOREPROVIDER

Carrega uma biblioteca do provedor de armazenamento de chaves para Always Encrypted ou recupera os nomes de bibliotecas do provedor de keystore carregado. Consulte [provedores de armazenamento de chaves personalizado](custom-keystore-providers.md) para obter mais informações. Esse atributo não tem valor padrão.

| Valor de atributo | Description |
|-|-|
| char * | Caminho para uma biblioteca de provedor de armazenamento de chaves |


