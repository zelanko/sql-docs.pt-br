---
title: Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: a4ba44733d2a14323f128f1ab105e79169b90cce
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75250944"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

Este exemplo demonstra o uso do Provedor do Azure Key Vault ao acessar colunas criptografadas.

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

## <a name="see-also"></a>Consulte Também

- [Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted](azure-key-vault-example.md)
- [Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [Como usar o Always Encrypted com o Provedor de Dados do Microsoft .NET para SQL Server](sqlclient-support-always-encrypted.md)
