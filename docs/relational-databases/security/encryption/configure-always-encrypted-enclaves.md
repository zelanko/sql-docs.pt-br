---
title: Configurar e usar o Always Encrypted com enclaves seguros | Microsoft Docs
description: Saiba como configurar e usar o Always Encrypted com enclaves seguros no SQL Server, que permite uma funcionalidade mais avançada sobre dados confidenciais.
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d73d337e750e287066531017710b733c92a312ff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627018"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>Configurar e usar o Always Encrypted com enclaves seguros 

[!INCLUDE[SQL Server 2019](../../../includes/applies-to-version/sqlserver2019.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) estende o recurso [Always Encrypted](always-encrypted-database-engine.md) existente para habilitar funcionalidades mais avançadas em dados confidenciais mantendo a confidencialidade desses dados. Este artigo lista tarefas comuns para configurar e usar o recurso.

Para ver um tutorial que mostra como começar rapidamente a usar o Always Encrypted com enclaves seguros, confira [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>Configurar seu ambiente para dar suporte a enclaves e atestado
Para obter detalhes, confira os seguintes artigos:
- [Planejar o atestado do Serviço Guardião de Host](./always-encrypted-enclaves-host-guardian-service-plan.md)
- [Implantar o Serviço Guardião de Host para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md)
- [Registrar seu computador com o Serviço Guardião de Host](./always-encrypted-enclaves-host-guardian-service-register.md)

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Gerenciar chaves para Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Gerenciar chaves para Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-manage-keys.md)
- [Provisionar chaves habilitadas para enclave](always-encrypted-enclaves-provision-keys.md)
- [Girar chaves habilitadas para enclave](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>Configurar colunas com o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-configure-encryption.md)
- [Configurar criptografia de coluna in-loco com Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)

> [!NOTE]
> Para obter um tutorial passo a passo sobre como configurar um ambiente de teste e experimentar a funcionalidade do Always Encrypted com enclaves seguras no SSMS, confira [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Consultar colunas usando o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Consultar colunas usando o Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-query-columns.md)
- [Consultar colunas usando o Always Encrypted com enclaves seguros com o SSMS](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>Criar e usar índices em colunas habilitadas para enclave
Confira os seguintes artigos para obter detalhes:
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)

## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Desenvolver aplicativos usando o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)
