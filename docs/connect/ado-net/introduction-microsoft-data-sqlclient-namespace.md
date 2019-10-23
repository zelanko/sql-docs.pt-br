---
title: Introdução ao namespace Microsoft.Data.SqlClient
description: Página de introdução para o namespace Microsoft. Data. SqlClient.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4f4034c557c13054dcfb6ed425ca996b0c5363f6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452386"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introdução ao namespace Microsoft.Data.SqlClient

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Download ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Esta página descreve como o namespace Microsoft. Data. SqlClient oferece funcionalidade adicional sobre o namespace System. Data. SqlClient existente.
  
## <a name="release-notes"></a>Notas de versão
Todas as notas de versão estão disponíveis no [repositório GitHub](https://github.com/dotnet/SqlClient/tree/master/release-notes).

## <a name="new-features"></a>Novos recursos

### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>Novos recursos em .NET Framework 4.7.2 System. Data. SqlClient

Classificação de dados – disponível no banco de dados SQL do Azure e Microsoft SQL Server 2019 desde o CTP 2,0.

Suporte a UTF-8-disponível em Microsoft SQL Server SQL Server 2019 desde o CTP 2,3.

### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>Novos recursos no .NET Core 2,2 System. Data. SqlClient

Classificação de dados – disponível no banco de dados SQL do Azure e Microsoft SQL Server 2019 desde o CTP 2,0.

Suporte a UTF-8-disponível em Microsoft SQL Server SQL Server 2019 desde o CTP 2,3.

Always Encrypted com enclaves-Always Encrypted está disponível no Microsoft SQL Server 2016 e superior. O suporte a enclave foi introduzido no Microsoft SQL Server 2019 CTP 2,0.

Autenticação-modo de autenticação de senha Active Directory.

### <a name="data-classification"></a>Classificação de dados

A classificação de dados traz um novo conjunto de APIs expondo informações de classificação e classificações de dados somente leitura sobre objetos recuperados via SqlDataReader quando a fonte subjacente dá suporte ao recurso e contém metadados sobre a [confidencialidade dos dados e classificação](../../relational-databases/security/sql-data-discovery-and-classification.md).

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

O suporte a UTF-8 não requer nenhuma alteração de código do aplicativo. Essas alterações de SqlClient simplesmente otimizam a comunicação entre o cliente e o servidor quando o servidor dá suporte a UTF-8 e o agrupamento de coluna subjacente é UTF-8. Consulte a seção UTF-8 em [novidades na versão prévia do SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted com enclaves

Em geral, a documentação existente que usa System. Data. SqlClient em .NET Framework **e provedores internos de repositório de chaves mestras de coluna** agora deve funcionar com o .NET Core.

 [Desenvolver usando o Always Encrypted com o Provedor de Dados .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: proteger dados confidenciais e armazenar chaves de criptografia no repositório de certificados do Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Autenticação

Modos de autenticação diferentes podem ser especificados usando a opção de cadeia de conexão de _autenticação_ . Para obter mais informações, consulte a [documentação de SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> Provedores de repositório de chaves personalizados, como o provedor de Azure Key Vault, precisarão ser atualizados para dar suporte a Microsoft. Data. SqlClient. Da mesma forma, os provedores de enclave também precisarão ser atualizados para dar suporte a Microsoft. Data. SqlClient.
> Always Encrypted só tem suporte em destinos do .NET Framework e do .NET Core. Não há suporte para ele em .NET Standard já que .NET Standard não tem determinadas dependências de criptografia.
