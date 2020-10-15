---
title: Introdução ao namespace Microsoft.Data.SqlClient
description: Saiba mais sobre o namespace Microsoft.Data.SqlClient e porque ele é a maneira preferida de se conectar ao SQL para aplicativos .NET.
ms.date: 09/29/2020
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: d02c12998f1083774727c33a261292396151a352
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081465"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introdução ao namespace Microsoft.Data.SqlClient

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

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