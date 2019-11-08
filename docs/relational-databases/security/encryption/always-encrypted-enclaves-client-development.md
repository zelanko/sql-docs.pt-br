---
title: Desenvolver aplicativos usando o Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 54e282e7d68c23837c1865f1257ba7e159644d26
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595531"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Desenvolver aplicativos usando o Always Encrypted com enclaves seguros
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) estende o [Always Encrypted](always-encrypted-database-engine.md) para habilitar uma funcionalidade mais rica das consultas de aplicativo em colunas de banco de dados confidenciais criptografadas. Ele aproveita as tecnologias de enclave seguro para permitir que o executor da consulta em [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] delegue cálculos em colunas criptografadas a um enclave seguro dentro do processo de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

## <a name="client-driver-for-always-encrypted-with-secure-enclaves"></a>Driver do cliente para Always Encrypted com enclaves seguros

Para desenvolver aplicativos usando o Always Encrypted com enclaves seguros, você precisa de uma versão do driver de cliente do SQL que dê suporte a enclaves seguros. O driver de cliente desempenha a seguinte função importante:
- Antes de enviar uma consulta que usa um enclave seguro para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para execução, o driver inicia o atestado do enclave para verificar se o enclave seguro é confiável e pode ser usado com segurança para processar dados confidenciais. Para obter mais informações sobre o atestado, confira [Atestado de enclave seguro](always-encrypted-enclaves.md#secure-enclave-attestation).
- Depois que o atestado for bem sucedido, o driver de cliente estabelecerá uma sessão segura com o enclave negociando um segredo compartilhado.
- O driver usa o segredo compartilhado para criptografar as chaves de criptografia de coluna de que o enclave precisará para processar a consulta e envia as chaves para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], que as encaminha para o enclave seguro que descriptografa as chaves. 
- Por fim, o driver envia a consulta para execução, i que dispara cálculos dentro do enclave seguro.

Para usar a funcionalidade do enclave seguro, você precisa configurar seu aplicativo e o driver de cliente para habilitar cálculos de enclave ao se conectar ao banco de dados e especificar um ponto de extremidade de serviço de atestado (uma URL de atestado enclave) que aponta para um serviço de atestado para seu enclave. Os detalhes dependem de um driver e do serviço/protocolo de atestado que você está usando.

## <a name="next-steps"></a>Próximas etapas

Os drivers de cliente a seguir são suporte ao Always Encrypted com enclaves seguros:
- Provedor de Dados do .NET Framework para SQL Server no .NET Framework 4.7.2 ou acima. 
    - Para obter mais informações, confira [Usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md).
    - Para obter um tutorial passo a passo, confira [Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)
- Microsoft ODBC Driver for SQL Server, versão 17.4 ou acima. 
    - Para obter mais informações, veja [Como usar Always Encrypted com o driver ODBC do Windows](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md). 
    - Para obter informações sobre como habilitar cálculos de enclave para uma conexão de banco de dados usando ODBC, confira a seção [Habilitar o Always Encrypted com enclaves seguros](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves).
