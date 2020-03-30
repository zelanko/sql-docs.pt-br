---
title: Palavras-chave de cadeia de conexão e DSN para o driver ODBC – SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/04/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-chojas
ms.author: v-jizho2
author: karinazhou
ms.openlocfilehash: bf9b755176913ad144781c5be0ad53150aedcd1b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76911240"
---
# <a name="dsn-and-connection-string-keywords-and-attributes"></a>Atributos e palavras-chave da cadeia de conexão e DSN

Esta página lista as palavras-chave para cadeias de conexão e DSNs e os atributos de conexão para SQLSetConnectAttr e SQLGetConnectAttr, disponíveis no ODBC Driver for SQL Server.

## <a name="supported-dsnconnection-string-keywords-and-connection-attributes"></a>Atributos de conexão e palavras-chave de cadeia de conexão/DSN com suporte

A tabela a seguir lista as palavras-chave e os atributos disponíveis para cada plataforma (L: Linux; M: Mac; W: Windows). Clique na palavra-chave ou no atributo para obter mais detalhes.

| Palavras-chave da cadeia de conexão/DSN | Atributo de conexão | Plataforma |
|-|-|-|
| [Addr](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Endereço](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [AnsiNPW](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ANSI_NPW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssansinpw) | LMW |
| [APP](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ApplicationIntent](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_APPLICATION_INTENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssapplicationintent) | LMW |
| [AttachDBFileName](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ATTACHDBFILENAME](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssattachdbfilename) | LMW |
| [Autenticação](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sql_copt_ss_authentication) | [SQL_COPT_SS_AUTHENTICATION](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sql_copt_ss_authentication) | LMW |
| [AutoTranslate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRANSLATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstranslate) | LMW |
| [ColumnEncryption](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sql_copt_ss_column_encryption) | [SQL_COPT_SS_COLUMN_ENCRYPTION](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sql_copt_ss_column_encryption) | LMW |
| [ConnectRetryCount](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_COUNT](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [ConnectRetryInterval](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_INTERVAL](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [Backup de banco de dados](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_ATTR_CURRENT_CATALOG](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| [Descrição](../../connect/odbc/dsn-connection-string-attribute.md#description) | | LMW |
| [Driver](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [DSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Encrypt](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ENCRYPT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssencrypt) | LMW |
| [Failover_Partner](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssfailoverpartner) | W |
| [FailoverPartnerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | W |
| [FileDSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [KeepAlive](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md) (v17.4+, somente DSN)| | LMW |
| [KeepAliveInterval](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md) (v17.4+, somente DSN) | | LMW |
| [KeystoreAuthentication](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystorePrincipalId](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystoreSecret](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [Idioma](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [MARS_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MARS_ENABLED](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmarsenabled) | LMW |
| [MultiSubnetFailover](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MULTISUBNET_FAILOVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmultisubnetfailover) | LMW |
| [Net](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Rede](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [PWD](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [QueryLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquery) | W |
| [QueryLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquerylog) | W |
| [QueryLogTIme](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_INTERVAL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfqueryinterval) | W |
| [QuotedId](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_QUOTED_IDENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssquotedident) | LMW |
| [Regional](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [SaveFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Servidor](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ServerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_SERVER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| [StatsLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdata) | W |
| [StatsLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalog) | W |
| [TransparentNetworkIPResolution](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sql_copt_ss_tnir) | [SQL_COPT_SS_TNIR](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sql_copt_ss_tnir) | LMW |
| [Trusted_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_INTEGRATED_SECURITY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssintegratedsecurity) | LMW |
| [TrustServerCertificate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRUST_SERVER_CERTIFICATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstrustservercertificate) | LMW |
| [UID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [UseFMTONLY](../../connect/odbc/dsn-connection-string-attribute.md#usefmtonly) | | LMW |
| [WSID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| | [SQL_ATTR_ACCESS_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ACCESS_MODE) | LMW |
| | [SQL_ATTR_ASYNC_DBC_EVENT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCALLBACK](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCONTEXT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
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
| | [SQL_COPT_SS_ACCESS_TOKEN](dsn-connection-string-attribute.md#sql_copt_ss_access_token) | LMW |
| | [SQL_COPT_SS_ANSI_OEM](dsn-connection-string-attribute.md#sql_copt_ss_ansi_oem)| W |
| | [SQL_COPT_SS_BCP](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbcp) | LMW |
| | [SQL_COPT_SS_BROWSE_CACHE_DATA](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) | LMW |
| | [SQL_COPT_SS_BROWSE_CONNECT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseconnect) | LMW |
| | [SQL_COPT_SS_BROWSE_SERVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseserver) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREDATA](dsn-connection-string-attribute.md#sql_copt_ss_cekeystoredata) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREPROVIDER](dsn-connection-string-attribute.md#sql_copt_ss_cekeystoreprovider) | LMW |
| | [SQL_COPT_SS_CLIENT_CONNECTION_ID](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) | LMW |
| | [SQL_COPT_SS_CONCAT_NULL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconcatnull) | LMW |
| | [SQL_COPT_SS_CONNECTION_DEAD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconnectiondead) | LMW |
| | [SQL_COPT_SS_ENLIST_IN_DTC](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistindtc) | W |
| | [SQL_COPT_SS_ENLIST_IN_XA](dsn-connection-string-attribute.md#sql_copt_ss_enlist_in_xa) | LMW |
| | [SQL_COPT_SS_FALLBACK_CONNECT](dsn-connection-string-attribute.md#sql_copt_ss_fallback_connect) | LMW |
| | [SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_MUTUALLY_AUTHENTICATED](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_OLDPWD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssoldpwd) | LMW |
| | [SQL_COPT_SS_PERF_DATA_LOG_NOW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalognow) | W |
| | [SQL_COPT_SS_PRESERVE_CURSORS](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsspreservecursors) | LMW |
| | [SQL_COPT_SS_SPID](../../connect/odbc/dsn-connection-string-attribute.md#sql_copt_ss_spid) (v17.5+) | LMW |
| | [SQL_COPT_SS_TXN_ISOLATION](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstxnisolation) | LMW |
| | [SQL_COPT_SS_USER_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssuserdata) | LMW |
| | [SQL_COPT_SS_WARN_ON_CP_ERROR](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsswarnoncperror) | LMW |
| [ClientCertificate](../../connect/odbc/dsn-connection-string-attribute.md#clientcertificate) | | LMW | 
| [ClientKey](../../connect/odbc/dsn-connection-string-attribute.md#clientkey) | | LMW | 


Aqui estão algumas palavras-chave de cadeia de conexão e os atributos de conexão que não estão documentados em [Usando palavras-chave de cadeia de conexão com SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md), [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [Função SQLSetConnectAttr](../../odbc/reference/syntax/sqlsetconnectattr-function.md).

### <a name="description"></a>DESCRIÇÃO

Usado para descrever a fonte de dados.

### <a name="sql_copt_ss_ansi_oem"></a>SQL_COPT_SS_ANSI_OEM

Controles para conversão de dados de ANSI em OEM. 

| Valor do atributo | DESCRIÇÃO |
|-|-|
| SQL_AO_OFF | (Padrão) Conversão não é executada. |
| SQL_AO_ON | Conversão é executada. |

### <a name="sql_copt_ss_fallback_connect"></a>SQL_COPT_SS_FALLBACK_CONNECT

Controla o uso de Conexões de Fallback do SQL Server. Esse atributo não tem mais suporte.

| Valor do atributo | DESCRIÇÃO |
|-|-|
| SQL_FB_OFF | (Padrão) Conexões de fallback estão desabilitadas. |
| SQL_FB_ON | Conexões de fallback estão habilitadas. |



## <a name="new-connection-string-keywords-and-connection-attributes"></a>Novos atributos de conexão e palavras-chave da cadeia de conexão

###  <a name="authentication---sql_copt_ss_authentication"></a>Autenticação – SQL_COPT_SS_AUTHENTICATION

Define o modo de autenticação a ser usado ao conectar-se ao SQL Server. Veja [Usando o Azure Active Directory](using-azure-active-directory.md) para obter mais informações.

| Valor de Palavra-Chave | Valor do atributo | DESCRIÇÃO |
|-|-|-|
| |SQL_AU_NONE|(Padrão) Não definido. A combinação de outros atributos determina o modo de autenticação.|
|SqlPassword|SQL_AU_PASSWORD|Autenticação do SQL Server com nome de usuário e senha.|
|ActiveDirectoryIntegrated|SQL_AU_AD_INTEGRATED|Autenticação Integrada do Azure Active Directory.|
|ActiveDirectoryPassword|SQL_AU_AD_PASSWORD|Autenticação da Senha do Azure Active Directory.|
|ActiveDirectoryInteractive|SQL_AU_AD_INTERACTIVE|Autenticação Interativa do Azure Active Directory.|
|ActiveDirectoryMsi|SQL_AU_AD_MSI|Autenticação de Identidade de Serviço Gerenciada do Azure Active Directory. Para identidade atribuída pelo usuário, o UID é definido como a ID de objeto da identidade do usuário. |
| |SQL_AU_RESET|Remover definição. Substitui qualquer configuração de cadeia de conexão ou DSN.|

> [!NOTE]
> Ao usar a palavra-chave ou atributo `Authentication`, especifique explicitamente a configuração `Encrypt` como o valor desejado na cadeia de conexão/DSN/atributo de conexão. Veja [Usando palavras-chave de cadeia de conexão com o SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) para obter detalhes.

### <a name="columnencryption---sql_copt_ss_column_encryption"></a>ColumnEncryption – SQL_COPT_SS_COLUMN_ENCRYPTION

Controla a criptografia de coluna transparente (Always Encrypted). Veja [Usando Always Encrypted (ODBC)](using-always-encrypted-with-the-odbc-driver.md) para obter mais informações.

| Valor de Palavra-Chave | Valor do atributo | DESCRIÇÃO |
|-|-|-|
|habilitado|SQL_CE_ENABLED|Habilita o Always Encrypted.|
|Desabilitado|SQL_CE_ENABLED|(Padrão) Desabilita o Always Encrypted.|
| |SQL_CE_RESULTSETONLY|Habilite somente descriptografia (resultados e valores retornados).|

### <a name="transparentnetworkipresolution---sql_copt_ss_tnir"></a>TransparentNetworkIPResolution – SQL_COPT_SS_TNIR

Controla o recurso de Resolução de IP de Rede Transparente, que interage com MultiSubnetFailover para permitir tentativas de reconexão mais rápidas. Veja [Usando resolução de IP de rede transparente](using-transparent-network-ip-resolution.md) para obter mais informações.

| Valor de Palavra-Chave | Valor do atributo| DESCRIÇÃO |
|-|-|-|
|habilitado|SQL_IS_ON|(Padrão) Habilita a resolução IP de rede transparente.|
|Desabilitado|SQL_IS_OFF|Desativa a resolução IP de rede transparente.|

### <a name="usefmtonly"></a>UseFMTONLY

Controla o uso de SET FMTONLY para metadados quando está se conectando ao SQL Server 2012 e versões mais recentes.

| Valor de Palavra-Chave | DESCRIÇÃO |
|-|-|
|Não|(Padrão) Use sp_describe_first_result_set para metadados, se disponível. |
|Sim| Use SET FMTONLY para metadados. |


## <a name="clientcertificate"></a>ClientCertificate

Especifica o certificado a ser usado para autenticação. As opções são: 

| Valor de Opção | DESCRIÇÃO |
|-|-|
| sha1:`<hash_value>` | O driver ODBC usa o hash SHA1 para localizar um certificado no Repositório de Certificados do Windows |
| assunto:`<subject>` | O driver ODBC usa o assunto para localizar um certificado no Repositório de Certificados do Windows |
| arquivo:`<file_location>`[,senha:`<password>`] | O driver ODBC usa um arquivo de certificado. |

Caso o certificado esteja no formato PFX e a chave privada dentro do certificado PFX esteja protegida por senha, a palavra-chave da senha será exigida. Para certificados nos formatos PEM e DER, o atributo ClientKey é exigido


## <a name="clientkey"></a>ClientKey

Especifica um local do arquivo da chave privada para certificados PEM ou DER especificados pelo atributo ClientCertificate. Formato: 

| Valor de Opção | DESCRIÇÃO |
|-|-|
| arquivo:`<file_location>`[,senha:`<password>`] | Especifica o local do arquivo de chave privada. |

Caso o arquivo de chave privada seja protegido por senha, a palavra-chave da senha será exigida. Se a senha contiver caracteres ",", um caractere "," extra será adicionado imediatamente após cada um deles. Por exemplo, se a senha for "a,b,c", a senha de escape presente na cadeia de conexão será "a,,b,,c". 
    

### <a name="sql_copt_ss_access_token"></a>SQL_COPT_SS_ACCESS_TOKEN

Permite o uso de um token de acesso do Azure Active Directory para autenticação. Veja [Usando o Azure Active Directory](using-azure-active-directory.md) para obter mais informações.

| Valor do atributo | DESCRIÇÃO |
|-|-|
| NULO | (Padrão) Nenhum token de acesso é fornecido. |
| ACCESSTOKEN* | Ponteiro para um token de acesso. |

### <a name="sql_copt_ss_cekeystoredata"></a>SQL_COPT_SS_CEKEYSTOREDATA

Comunica-se com uma biblioteca de provedor de repositório de chaves carregada. Veja Controla a criptografia de coluna transparente (Always Encrypted). Esse atributo não tem valor padrão. Veja [Provedores do Repositório de Chaves Personalizado](custom-keystore-providers.md) para obter mais informações.

| Valor do atributo | DESCRIÇÃO |
|-|-|
| CEKEYSTOREDATA * | Estrutura de dados de comunicação para a biblioteca do provedor de repositório de chaves |

### <a name="sql_copt_ss_cekeystoreprovider"></a>SQL_COPT_SS_CEKEYSTOREPROVIDER

Carrega uma biblioteca de provedor de repositório de chaves para Always Encrypted ou recupera os nomes das bibliotecas de provedor de repositório de chaves carregadas. Veja [Provedores do Repositório de Chaves Personalizado](custom-keystore-providers.md) para obter mais informações. Esse atributo não tem valor padrão.

| Valor do atributo | DESCRIÇÃO |
|-|-|
| char * | Caminho para uma biblioteca de provedores de repositório de chaves |

### <a name="sql_copt_ss_enlist_in_xa"></a>SQL_COPT_SS_ENLIST_IN_XA

Para habilitar transações XA com um TP (Processador de Transações) em conformidade com XA, o aplicativo precisa chamar **SQLSetConnectAttr** com SQL_COPT_SS_ENLIST_IN_XA e um ponteiro para um objeto `XACALLPARAM`. Essa opção tem suporte no Windows, no Linux (17.3 e superiores) e no Mac.
```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, param, SQL_IS_POINTER);  // XACALLPARAM *param
``` 
 Para associar uma transação XA a apenas uma conexão ODBC, forneça TRUE ou FALSE com SQL_COPT_SS_ENLIST_IN_XA, em vez do ponteiro, ao chamar **SQLSetConnectAttr**. Isso só é válido no Windows e não pode ser usado para especificar as operações de XA por meio de um aplicativo cliente. 
 ```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, (SQLPOINTER)TRUE, 0);
``` 

|Valor|DESCRIÇÃO|Plataformas|  
|-----------|-----------------|-----------------|  
|Objeto XACALLPARAM*|O ponteiro para o objeto `XACALLPARAM`.|Windows, Linux e Mac|
|TRUE|Associa a transação XA à conexão ODBC. Todas as atividades de banco de dados relacionadas serão executadas sob a proteção da transação XA.|Windows|  
|FALSE|Associa a transação à conexão ODBC.|Windows|

 Veja [Usando transações XA](../../connect/odbc/use-xa-with-dtc.md) para obter mais informações sobre transações XA.

### <a name="sql_copt_ss_spid"></a>SQL_COPT_SS_SPID

Recupera a ID do processo do servidor da conexão. Isso equivale à variável T-SQL [@@SPID](../../t-sql/functions/spid-transact-sql.md), exceto pelo fato de que ela não incorre em uma viagem de ida e volta adicional ao servidor.

| Valor do atributo | DESCRIÇÃO |
|-|-|
| DWORD | SPID |
