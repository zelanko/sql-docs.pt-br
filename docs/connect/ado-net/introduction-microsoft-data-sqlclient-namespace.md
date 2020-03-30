---
title: Introdução ao namespace Microsoft.Data.SqlClient
description: Página de introdução ao namespace Microsoft.Data.SqlClient.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: dbc76f1a2ee93faf642d923d3a543eee40d5348b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897126"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introdução ao namespace Microsoft.Data.SqlClient

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Notas sobre a versão do Microsoft.Data.SqlClient 1.1.0

As notas sobre a versão também estão disponíveis no repositório GitHub: [Notas sobre a versão 1.1](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>Novos recursos

#### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros

O Always Encrypted está disponível no Microsoft SQL Server 2016 e em versões posteriores. Os enclaves seguros estão disponíveis no Microsoft SQL Server 2019 e em versões posteriores. Para usar o recurso de enclave, as cadeias de conexão devem incluir o protocolo de atestado e a URL de atestado necessários. Exemplos:

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

A classificação de dados traz um novo conjunto de APIs expondo informações de classificação e a confidencialidade de dados somente leitura sobre objetos recuperados via SqlDataReader quando a fonte subjacente dá suporte ao recurso e contém metadados sobre [classificação e confidencialidade de dados](../../relational-databases/security/sql-data-discovery-and-classification.md).

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

O suporte a UTF-8 não requer nenhuma alteração de código do aplicativo. Essas alterações de SqlClient simplesmente otimizam a comunicação entre o cliente e o servidor quando o servidor dá suporte a UTF-8 e a ordenação de coluna subjacente é UTF-8. Confira a seção UTF-8 em [Novidades na versão prévia do SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted com enclaves

Em geral, a documentação existente que usa System.Data.SqlClient no .NET Framework **e provedores internos de repositório de chaves mestras de coluna** agora deve funcionar também com o .NET Core.

 [Desenvolver usando o Always Encrypted com o Provedor de Dados .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: Proteger dados confidenciais e armazenar chaves de criptografia no repositório de certificados do Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Autenticação

Modos de autenticação diferentes podem ser especificados usando a opção de cadeia de conexão _Authentication_. Para obter mais informações, confira a [documentação do SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> Provedores de repositório de chaves personalizados, como o provedor do Azure Key Vault, precisarão ser atualizados para dar suporte a Microsoft.Data.SqlClient. Da mesma forma, os provedores de enclave também precisarão ser atualizados para dar suporte ao Microsoft.Data.SqlClient.
> O Always Encrypted só é compatível com destinos do .NET Framework e do .NET Core. Ele não é compatível com o .NET Standard, já que o .NET Standard não tem determinadas dependências de criptografia.
