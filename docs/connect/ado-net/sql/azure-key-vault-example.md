---
title: Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted | Microsoft Docs
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
ms.openlocfilehash: fca498fbc7f79dcfc8852799ade6e230952ea082
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250951"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

Este exemplo demonstra o uso do Provedor do Azure Key Vault ao acessar colunas criptografadas.

[!code-csharp [AKVProvider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

## <a name="see-also"></a>Consulte Também

- [Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros](azure-key-vault-enclave-example.md)
- [Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [Como usar o Always Encrypted com o Provedor de Dados do Microsoft .NET para SQL Server](sqlclient-support-always-encrypted.md)
