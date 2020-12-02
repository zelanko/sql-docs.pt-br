---
description: Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted
title: Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2020
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 51c99e679855ca762b7adc5763086b4ded9b6cf5
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2020
ms.locfileid: "96123884"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

Este exemplo demonstra o uso do Provedor do Azure Key Vault ao acessar colunas criptografadas.

[!code-csharp [AKVProvider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

> [!NOTE]
> - Para usar o recurso Always Encrypted sem enclaves seguros para o aplicativo .NET Standard, é necessário o **Microsoft.Data.SqlClient** versão 2.1.0 ou posterior. A versão do .NET Standard com suporte é a 2.0 ou posterior. 
>
> - Para usar o recurso Always Encrypted no Linux ou macOS, é necessário o **Microsoft.Data.SqlClient** versão 2.1.0 ou posterior.

## <a name="see-also"></a>Consulte Também

- [Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros](azure-key-vault-enclave-example.md)
- [Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [Como usar o Always Encrypted com o Provedor de Dados do Microsoft .NET para SQL Server](sqlclient-support-always-encrypted.md)
