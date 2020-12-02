---
title: Introdução ao namespace Microsoft.Data.SqlClient
description: Saiba mais sobre o namespace Microsoft.Data.SqlClient e porque ele é a maneira preferida de se conectar ao SQL para aplicativos .NET.
ms.date: 11/19/2020
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: f522b856e759ec9821b5cc549ce3f801951b7283
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2020
ms.locfileid: "95011830"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introdução ao namespace Microsoft.Data.SqlClient

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-21"></a>Notas sobre a versão do Microsoft.Data.SqlClient 2.1

As notas sobre a versão também estão disponíveis no repositório GitHub: [Notas sobre a versão 2.1](https://github.com/dotnet/SqlClient/tree/master/release-notes/2.1).

### <a name="new-features"></a>Novos recursos

### <a name="cross-platform-support-for-always-encrypted"></a>Suporte multiplataforma ao Always Encrypted
O Microsoft. Data.SqlClient v2.1 estende o suporte ao Always Encrypted nas seguintes plataformas:

| Suporte ao Always Encrypted | Suporte ao Always Encrypted com enclaves seguros  | Estrutura de Destino | Versão do Microsoft.Data.SqlClient | Sistema operacional |
|:--|:--|:--|:--:|:--:|
| Sim | Sim | .NET Framework 4.6 ou versão posterior | 1.1.0+ | Windows |
| Sim | Sim | .NET Core 2.1+ | 2.1.0+<sup>1</sup> | Windows, Linux, macOS |
| Yes | Não<sup>2</sup> | .NET Standard 2.0 | 2.1.0+ | Windows, Linux, macOS |
| Sim | Sim | .NET Standard 2.1+ | 2.1.0+ | Windows, Linux, macOS |

> [!NOTE]
> <sup>1</sup> Antes da versão v2.1 do Microsoft.Data.SqlClient, só há suporte para o Always Encrypted no Windows.
> <sup>2</sup> O Always Encrypted com enclaves seguros tem suporte apenas no .NET Standard 2.0.

### <a name="azure-active-directory-device-code-flow-authentication"></a>Autenticação de fluxo de código do dispositivo do Azure Active Directory
O Microsoft.Data.SqlClient v 2.1 dá suporte à autenticação de "fluxo de código do dispositivo" com o MSAL.NET.
Documentação de referência: [Fluxo de concessão de autorização do dispositivo OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-device-code)

Exemplo de cadeia de conexão:

`Server=<server>.database.windows.net; Authentication=Active Directory Device Code Flow; Database=Northwind;`

A seguinte API permite a personalização do mecanismo de retorno de chamada do fluxo de código do dispositivo:

```csharp
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework, .NET Core and .NET Standard targeted applications
    public void SetDeviceCodeFlowCallback(Func<DeviceCodeResult, Task> deviceCodeFlowCallbackMethod)
}
```

### <a name="azure-active-directory-managed-identity-authentication"></a>Autenticação de Identidade Gerenciada do Azure Active Directory
O Microsoft.Data.SqlClient v 2.1 apresenta o suporte para autenticação do Azure Active Directory usando [identidades gerenciadas](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

Há suporte para as seguintes palavras-chave de modo de autenticação:
- Identidade gerenciada do Active Directory
- MSI do Active Directory (para compatibilidade entre drivers do MS SQL)

Exemplos de cadeia de conexão:

```cs
// For System Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory MSI; Initial Catalog={db};"

// For System Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory Managed Identity; Initial Catalog={db};"

// For User Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory MSI; User Id={ObjectIdOfManagedIdentity}; Initial Catalog={db};"

// For User Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory Managed Identity; User Id={ObjectIdOfManagedIdentity}; Initial Catalog={db};"
```

### <a name="azure-active-directory-interactive-authentication-enhancements"></a>Aprimoramentos de autenticação interativa do Azure Active Directory
O Microsoft.Data.SqlClient v2.1 adiciona as seguintes APIs para personalizar a experiência de autenticação "interativa do Active Directory":

```csharp
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework targeted applications only
    public void SetIWin32WindowFunc(Func<IWin32Window> iWin32WindowFunc);

    // For .NET Standard targeted applications only
    public void SetParentActivityOrWindowFunc(Func<object> parentActivityOrWindowFunc);

    // For .NET Framework, .NET Core and .NET Standard targeted applications
    public void SetAcquireAuthorizationCodeAsyncCallback(Func<Uri, Uri, CancellationToken, Task<Uri>> acquireAuthorizationCodeAsyncCallback);

    // For .NET Framework, .NET Core and .NET Standard targeted applications
    public void ClearUserTokenCache();
}
```

### <a name="sqlclientauthenticationproviders-configuration-section"></a>Seção de configuração `SqlClientAuthenticationProviders`
O Microsoft.Data.SqlClient v2.1 introduz uma nova seção de configuração, `SqlClientAuthenticationProviders` (um clone da `SqlAuthenticationProviders`existente). A seção de configuração existente, `SqlAuthenticationProviders`, ainda tem suporte para compatibilidade com versões anteriores quando o tipo apropriado é definido.

A nova seção permite que os arquivos de configuração de aplicativo contenham uma seção SqlAuthenticationProviders para System.Data.SqlClient e uma seção SqlClientAuthenticationProviders para Microsoft.Data.SqlClient.


### <a name="azure-active-directory-authentication-using-an-application-client-id"></a>Autenticação do Azure Active Directory usando uma ID do cliente do aplicativo
O Microsoft.Data.SqlClient v2.1 introduz o suporte para transmitir uma ID do cliente do aplicativo definida pelo usuário à Biblioteca de Autenticação da Microsoft. A ID do cliente do aplicativo é usada na autenticação com o Azure Active Directory.

Introdução das seguintes novas APIs:

1. Foi introduzida uma nova em ActiveDirectoryAuthenticationProvider:\
_[Aplica-se a todas as plataformas .NET (.NET Framework, .NET Core e .NET Standard)]_

```csharp
public ActiveDirectoryAuthenticationProvider(string applicationClientId)
```

Uso:
```csharp
string APP_CLIENT_ID = "<GUID>";
SqlAuthenticationProvider customAuthProvider = new ActiveDirectoryAuthenticationProvider(APP_CLIENT_ID);
SqlAuthenticationProvider.SetProvider(SqlAuthenticationMethod.ActiveDirectoryInteractive, customAuthProvider);

using (SqlConnection sqlConnection = new SqlConnection("<connection_string>")
{
    sqlConnection.Open();
}
```

2. Uma nova propriedade de configuração foi introduzida em `SqlAuthenticationProviderConfigurationSection` e `SqlClientAuthenticationProviderConfigurationSection`:\
_[Aplica-se a .NET Framework e .NET Core]_

```csharp
internal class SqlAuthenticationProviderConfigurationSection : ConfigurationSection
{
    ...
    [ConfigurationProperty("applicationClientId", IsRequired = false)]
    public string ApplicationClientId => this["applicationClientId"] as string;
}

// Inheritance
internal class SqlClientAuthenticationProviderConfigurationSection : SqlAuthenticationProviderConfigurationSection
{ ... }
```

Uso:
```xml
<configuration>
    <configSections>
        <section name="SqlClientAuthenticationProviders"
                         type="Microsoft.Data.SqlClient.SqlClientAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
    </configSections>
    <SqlClientAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>

<!--or-->

<configuration>
    <configSections>
        <section name="SqlAuthenticationProviders"
                         type="Microsoft.Data.SqlClient.SqlAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
    </configSections>
    <SqlAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>
```

### <a name="data-classification-v2-support"></a>Suporte para classificação de dados v2
O Microsoft.Data.SqlClient v2.1 apresenta suporte para informações de "classificação de confidencialidade" da classificação de dados. Agora estão disponíveis as seguintes novas APIs:

```csharp
public class SensitivityClassification
{
    public SensitivityRank SensitivityRank;
}

public class SensitivityProperty
{
    public SensitivityRank SensitivityRank;
}

public enum SensitivityRank
{
    NOT_DEFINED = -1,
    NONE = 0,
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30,
    CRITICAL = 40
}
```

### <a name="server-process-id-for-an-active-sqlconnection"></a>ID do processo do servidor para uma `SqlConnection` ativa
O Microsoft.Data.SqlClient v2.1 introduz uma nova propriedade `SqlConnection`, `ServerProcessId`, em uma conexão ativa.

```csharp
public class SqlConnection
{
    // Returns the server process Id (SPID) of the active connection.
    public int ServerProcessId;
}
```

### <a name="trace-logging-support-in-native-sni"></a>Suporte ao registro em log de rastreamento no SNI nativo
O Microsoft.Data.SqlClient v2.1 estende a implementação da `SqlClientEventSource` existente para habilitar o rastreamento de eventos em SNI.dll. Os eventos devem ser capturados usando uma ferramenta como XPerf.

O rastreamento pode ser habilitado enviando um comando para `SqlClientEventSource` conforme ilustrado abaixo:

```csharp
// Enables trace events:
EventSource.SendCommand(eventSource, (EventCommand)8192, null);

// Enables flow events:
EventSource.SendCommand(eventSource, (EventCommand)16384, null);

// Enables both trace and flow events:
EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
```


### <a name="command-timeout-connection-string-property"></a>Propriedade de cadeia de conexão "Tempo limite do comando"
O Microsoft.Data.SqlClient v2.1 apresenta a propriedade de cadeia de conexão "Tempo limite do comando" para substituir o padrão de 30 segundos. O tempo limite para comandos individuais pode ser substituído usando a propriedade `CommandTimeout` no SqlCommand.

Exemplos de cadeia de conexão:

`"Server={serverURL}; Initial Catalog={db}; Integrated Security=true; Command Timeout=60"`

### <a name="removal-of-symbols-from-native-sni"></a>Remoção de símbolos do SNI nativo
Com o Microsoft.Data.SqlClient v2.1, removemos os símbolos introduzidos na [v2.0.0](https://www.nuget.org/packages/Microsoft.Data.SqlClient.SNI/2.0.0) do NuGet do [Microsoft.Data.SqlClient.SNI.Runtime](https://www.nuget.org/packages/Microsoft.Data.SqlClient.SNI.runtime) começando com a [v2.1.1](https://www.nuget.org/packages/Microsoft.Data.SqlClient.SNI.runtime/2.1.1). Os símbolos públicos agora são publicados no servidor de símbolos da Microsoft para ferramentas como BinSkim que exigem acesso a símbolos públicos.

### <a name="source-linking-of-microsoftdatasqlclient-symbols"></a>Vinculação à fonte de símbolos do Microsoft.Data.SqlClient
A partir do Microsoft.Data.SqlClient v2.1, os símbolos do Microsoft.Data.SqlClient são vinculados à fonte e publicados no servidor de símbolos da Microsoft para uma experiência de depuração avançada sem a necessidade de baixar o código-fonte.


## <a name="release-notes-for-microsoftdatasqlclient-20"></a>Notas sobre a versão do Microsoft.Data.SqlClient 2.0

As notas sobre a versão também estão disponíveis no repositório GitHub: [2.0 Notas sobre a versão](https://github.com/dotnet/SqlClient/tree/master/release-notes/2.0).

### <a name="breaking-changes"></a>Alterações de quebra

- O modificador de acesso para a interface do provedor de enclave `SqlColumnEncryptionEnclaveProvider` foi alterado de `public` para `internal`.

- As constantes na classe `SqlClientMetaDataCollectionNames` foram atualizadas para refletir as alterações no SQL Server.

- O driver agora executará a validação do Certificado do Servidor quando o SQL Server de destino impor a criptografia TLS, que é a padrão para conexões do Azure.

- `SqlDataReader.GetSchemaTable()` agora retorna uma `DataTable` vazia em vez de `null`.

- O driver agora executa o arredondamento de escala decimal para corresponder ao comportamento do SQL Server. Para compatibilidade com versões anteriores, o comportamento anterior de truncamento pode ser habilitado usando um comutador AppContext.

- Para aplicativos .NET Framework que consomem **Microsoft.Data.SqlClient**, os arquivos SNI.dll baixados anteriormente nas pastas `bin\x64` e `bin\x86` agora são chamados `Microsoft.Data.SqlClient.SNI.x64.dll` e` Microsoft.Data.SqlClient.SNI.x86.dll` e serão baixados no diretório `bin`.

- Novos sinônimos de propriedade de cadeia de conexão substituirão as propriedades antigas ao buscar uma cadeia de conexão de `SqlConnectionStringBuilder` para fins de consistência. [Leia mais](#new-connection-string-property-synonyms)

### <a name="new-features"></a>Novos recursos

#### <a name="dns-failure-resiliency"></a>Resiliência de falha de DNS

O driver agora armazenará em cache os endereços IP de cada conexão bem-sucedida com um ponto de extremidade do SQL Server que ofereça suporte ao recurso. Se ocorrer uma falha de resolução de DNS durante uma tentativa de conexão, o driver tentará estabelecer uma conexão usando um endereço IP em cache para esse servidor, se existir algum.

#### <a name="eventsource-tracing"></a>Rastreamento de EventSource

Esta versão introduz suporte para capturar logs de rastreamento de eventos para depuração de aplicativos. Para capturar esses eventos, os aplicativos cliente devem escutar eventos da implementação EventSource do SqlClient:

```
Microsoft.Data.SqlClient.EventSource
```

Para obter mais informações, confira como [Habilitar o rastreamento de eventos no SqlClient](enable-eventsource-tracing.md).

#### <a name="enabling-managed-networking-on-windows"></a>Habilitando a rede gerenciada no Windows

Uma nova opção de AppContext, **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** , permite o uso de uma implementação de SNI gerenciado no Windows para fins de teste e depuração. Essa opção alternará o comportamento do driver para usar um SNI gerenciado nos projetos de .NET Core 2.1+ e .NET Standard 2.0+ no Windows, eliminando todas as dependências de bibliotecas nativas para a biblioteca Microsoft.Data.SqlClient.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

Confira [Opções de AppContext no SqlClient](appcontext-switches.md) para obter uma lista completa de opções disponíveis no driver.

#### <a name="enabling-decimal-truncation-behavior"></a>Habilitar o comportamento de truncamento de decimal

A escala de dados decimal será arredondada pelo driver por padrão, como é feito pelo SQL Server. Para compatibilidade com versões anteriores, você pode definir a opção AppContext **"Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal"** como **true**.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

#### <a name="new-connection-string-property-synonyms"></a>Novos sinônimos de propriedade de cadeia de conexão

Novos sinônimos foram adicionados para as propriedades de cadeia de conexão existentes a seguir para evitar a confusão de espaçamento em relação a propriedades com mais de uma palavra. Nomes de propriedade antigos continuarão com suporte por questão de compatibilidade com versões anteriores, mas as novas propriedades de cadeia de conexão serão incluídas ao buscar a cadeia de conexão de [SqlConnectionStringBuilder](/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder).

|Propriedade de cadeia de conexão existente|Novo sinônimo|
|-----------------------------------|-----------|
| ApplicationIntent | Tentativa de aplicativo |
| ConnectRetryCount | Contagem de repetições de conexão |
| ConnectRetryInterval | Intervalo de repetição de conexão |
| PoolBlockingPeriod | Período de bloqueio do pool |
| MultipleActiveResultSets | Conjuntos de resultados ativos múltiplos |
| MultiSubnetFailover | Failover de várias sub-redes |
| TransparentNetworkIPResolution | Resolução IP de Rede Transparente |
| TrustServerCertificate | Confiar em Certificado do Servidor |

#### <a name="sqlbulkcopy-rowscopied-property"></a>Propriedade SqlBulkCopy RowsCopied

A Propriedade RowsCopied fornece acesso somente leitura ao número de linhas que foram processadas na operação de cópia em massa em andamento. Esse valor pode não ser necessariamente igual ao número final de linhas adicionadas à tabela de destino.

#### <a name="connection-open-overrides"></a>Substituições abertas de conexão

O comportamento padrão de SqlConnection.Open() pode ser substituído para desabilitar o atraso de dez segundos e as tentativas de conexão automática disparadas por erros transitórios.

```csharp
using SqlConnection sqlConnection = new SqlConnection("Data Source=(local);Integrated Security=true;Initial Catalog=AdventureWorks;");
sqlConnection.Open(SqlConnectionOverrides.OpenWithoutRetry);
```

> [!NOTE]
> Observe que essa substituição só pode ser aplicada a SqlConnection.Open() e não a SqlConnection.OpenAsync().

#### <a name="username-support-for-active-directory-interactive-mode"></a>Suporte de nome de usuário para o modo interativo do Active Directory

Um nome de usuário pode ser especificado na cadeia de conexão ao usar o modo de autenticação interativa do Azure Active Directory para .NET Framework e .NET Core

Defina um nome de usuário usando a propriedade de cadeia de conexão **ID de Usuário** ou **UID**:

```
"Server=<server name>; Database=<db name>; Authentication=Active Directory Interactive; User Id=<username>;"
```

#### <a name="order-hints-for-sqlbulkcopy"></a>Dicas de ordem para SqlBulkCopy

As dicas de ordem podem ser fornecidas para aprimorar o desempenho de operações de cópia em massa em tabelas com índices clusterizados. Para obter mais informações, confira a seção [operações de cópia em massa](sql/bulk-copy-order-hints.md).

#### <a name="sni-dependency-changes"></a>Alterações de dependência de SNI

A Microsoft.Data.SqlClient (.NET Core e .NET Standard) no Windows agora é dependente da **Microsoft.Data.SqlClient.SNI.runtime**, substituindo a dependência anterior de **runtime.native.System.Data.SqlClient.SNI**. A nova dependência adiciona suporte para a plataforma do ARM junto com as plataformas já compatíveis ARM64, x64 e x86 no Windows.

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Notas sobre a versão do Microsoft.Data.SqlClient 1.1.0

As notas sobre a versão também estão disponíveis no repositório GitHub: [Notas sobre a versão 1.1](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>Novos recursos

#### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros

O Always Encrypted está disponível no Microsoft SQL Server 2016 e em versões posteriores. Os enclaves seguros estão disponíveis no Microsoft SQL Server 2019 e em versões posteriores. Para usar o recurso de enclave, as cadeias de conexão devem incluir o protocolo de atestado e a URL de atestado necessários. Por exemplo:

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

Para obter mais informações, consulte:

- [Suporte do SqlClient para Always Encrypted](sql/sqlclient-support-always-encrypted.md)
- [Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros](sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)

## <a name="release-notes-for-microsoftdatasqlclient-10"></a>Notas sobre a versão do Microsoft.Data.SqlClient 1.0

A versão inicial do namespace Microsoft.Data.SqlClient oferece funcionalidade adicional no namespace System.Data.SqlClient existente.
As notas sobre a versão também estão disponíveis no repositório GitHub: [Notas sobre a versão 1.0](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.0).

### <a name="new-features"></a>Novos recursos

#### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>Novos recursos no .NET Framework 4.7.2 System.Data.SqlClient

- **Classificação de dados** – disponível no Banco de Dados SQL do Azure e no Microsoft SQL Server 2019.

- **Suporte a UTF-8** – disponível no Microsoft SQL Server 2019.

#### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>Novos recursos no .NET Core 2.2 System.Data.SqlClient

- **Classificação de dados** – disponível no Banco de Dados SQL do Azure e no Microsoft SQL Server 2019.

- **Suporte a UTF-8** – disponível no Microsoft SQL Server 2019.

- **Autenticação** – modo de autenticação de senha do Active Directory.

### <a name="data-classification"></a>Classificação de dados

A classificação de dados traz um novo conjunto de APIs expondo informações de classificação e a confidencialidade de dados somente leitura sobre objetos recuperados via SqlDataReader quando a fonte subjacente dá suporte ao recurso e contém metadados sobre [classificação e confidencialidade de dados](../../relational-databases/security/sql-data-discovery-and-classification.md). Confira o aplicativo de exemplo em [Descoberta de dados e classificação no SqlClient](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

```csharp
public class SqlDataReader
{
    public Microsoft.Data.SqlClient.DataClassification.SensitivityClassification SensitivityClassification
}

namespace Microsoft.Data.SqlClient.DataClassification
{
    public class ColumnSensitivity
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.SensitivityProperty> SensitivityProperties
    }
    public class InformationType
    {
        public string Id
        public string Name
    }
    public class Label
    {
        public string Id
        public string Name
    }
    public class SensitivityClassification
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.ColumnSensitivity> ColumnSensitivities
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.InformationType> InformationTypes
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.Label> Labels
    }
    public class SensitivityProperty
    {
        public Microsoft.Data.SqlClient.DataClassification.InformationType InformationType
        public Microsoft.Data.SqlClient.DataClassification.Label Label
    }
}
```

### <a name="utf-8-support"></a>Suporte para UTF-8

O suporte a UTF-8 não requer nenhuma alteração de código do aplicativo. Essas alterações do SqlClient simplesmente otimizam a comunicação entre o cliente e o servidor quando o servidor é compatível com UTF-8 e a ordenação de coluna subjacente é UTF-8. Confira a seção UTF-8 em [Novidades no SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted com enclaves

Em geral, a documentação existente que usa System.Data.SqlClient no .NET Framework **e provedores internos de repositório de chaves mestras de coluna** agora devem funcionar também com o .NET Core.

 [Desenvolver usando o Always Encrypted com o Provedor de Dados .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: Proteger dados confidenciais e armazenar chaves de criptografia no repositório de certificados do Windows](/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Autenticação

Modos de autenticação diferentes podem ser especificados usando a opção de cadeia de conexão _Authentication_. Para obter mais informações, confira a [documentação do SqlAuthenticationMethod](/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2&preserve-view=true).

> [!NOTE]
> Provedores de repositório de chaves personalizados, como o provedor do Azure Key Vault, precisarão ser atualizados para dar suporte a Microsoft.Data.SqlClient. Da mesma forma, os provedores de enclave também precisarão ser atualizados para dar suporte ao Microsoft.Data.SqlClient.
> O Always Encrypted só é compatível com destinos do .NET Framework e do .NET Core. Ele não é compatível com o .NET Standard, já que o .NET Standard não tem determinadas dependências de criptografia.
