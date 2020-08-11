---
title: Opções de AppContext no SqlClient
description: Descreve como usar as opções de AppContext disponíveis no SqlClient.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 16d3ed6db478f12157333badf93682eb861c57f3
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091683"
---
# <a name="appcontext-switches-in-sqlclient"></a>Opções de AppContext no SqlClient

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

A classe AppContext permite que o SqlClient forneça novas funcionalidades enquanto continua dando suporte a chamadores que dependem do comportamento anterior. Os usuários podem recusar alterações no comportamento definindo opções de AppContext específicas.

## <a name="enabling-decimal-truncation-behavior"></a>Habilitando o comportamento de truncamento de decimal

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

Começando com o Microsoft.Data.SqlClient 2.0, os dados decimais serão arredondados por padrão, como é feito pelo SQL Server. Para habilitar o comportamento de truncamento anterior, você pode definir a opção de AppContext **"Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal"** como `true` na inicialização do aplicativo:

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

## <a name="enabling-managed-networking-on-windows"></a>Habilitando a rede gerenciada no Windows

[!INCLUDE [appliesto-xxxx-netcore-netst-md](../../includes/appliesto-xxxx-netcore-netst-md.md)]

No Windows, o SqlClient usa uma implementação nativa da interface de rede SNI por padrão. Para habilitar o uso de uma implementação de SNI gerenciada, você pode definir a opção de AppContext **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** como `true` na inicialização do aplicativo:

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

Essa opção alternará o comportamento do driver para usar a implementação de rede gerenciada em projetos do .NET Core 2.1+ e do .NET Standard 2.0+ no Windows, eliminando todas as dependências de bibliotecas nativas para a biblioteca Microsoft.Data.SqlClient. Ela tem finalidade apenas de teste e depuração.

> [!NOTE]
> Há algumas diferenças conhecidas em comparação com a implementação nativa. Por exemplo, a implementação gerenciada não dá suporte à Autenticação do Windows fora do domínio.

## <a name="disabling-transparent-network-ip-resolution"></a>Desabilitando a Resolução IP de Rede Transparente

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

A TNIR (Resolução IP de Rede Transparente) é uma revisão do recurso MultiSubnetFailover existente. A TNIR afeta a sequência de conexão do driver quando o primeiro IP resolvido do nome do host não responder e quando existem vários IPs associados ao nome do host. Ela interage com MultiSubnetFailover para fornecer as três seguintes sequências de conexão:<br />
* 0: um IP é tentado, seguido por todos os IPs em paralelo
* 1: todos os IPs são tentados em paralelo
* 2: todos os IPs são tentados um após o outro

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
|--------|--------|--------|
|True|True|1|
|True|Falso|0|
|Falso|True|1|
|Falso|Falso|2|

TransparentNetworkIPResolution é habilitado por padrão. MultiSubnetFailover é desabilitado por padrão. Para desabilitar a TNIR, você pode definir a opção de AppContext **"Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString"** como `true` na inicialização do aplicativo:

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString", true);
```

Para obter mais informações sobre como definir essas propriedades, confira a documentação da [Propriedade SqlConnection.ConnectionString](https://docs.microsoft.com/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring). 

## <a name="enable-a-minimum-timeout-during-login"></a>Habilitar um tempo limite mínimo durante o logon

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

Para evitar que uma tentativa de logon aguarde indefinidamente, você pode definir a opção de AppContext **Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin** como `true` na inicialização do aplicativo:

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin", false);
```

## <a name="disable-blocking-behavior-of-readasync"></a>Desabilitar o comportamento de bloqueio do ReadAsync

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

Por padrão, ReadAsync é executado de maneira síncrona e bloqueia o thread de chamada em .NET Framework. Para desabilitar esse comportamento de bloqueio, você pode definir a opção de AppContext **Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking** como `false` na inicialização do aplicativo:

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking", false);
```

## <a name="see-also"></a>Confira também

[Classe AppContext](https://docs.microsoft.com/dotnet/api/system.appcontext?view=netcore-3.1)
