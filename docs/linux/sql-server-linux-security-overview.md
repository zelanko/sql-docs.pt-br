---
title: Limitações de segurança para SQL Server em Linux
description: Saiba mais sobre as restrições do SQL Server em Linux, incluindo como o uso de chaves armazenadas no Azure Key Vault e o gerenciamento extensível de chaves que não têm suporte.
author: VanMSFT
ms.author: vanto
ms.date: 09/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 611afe6c02e979c7c9672d7d94f84844b8932cf6
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088785"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitações de segurança para SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

O SQL Server em Linux atualmente tem as seguintes limitações:

* Uma política de senha padrão é fornecida. MUST_CHANGE é a única opção que você pode configurar. A opção CHECK_POLICY não é compatível.
* Não há suporte para o Gerenciamento Extensível de Chaves. 
* Não há suporte para o uso de chaves armazenadas no Azure Key Vault.
* O SQL Server gera seu próprio certificado autoassinado para criptografar conexões. O SQL Server pode ser configurado para usar um certificado fornecido pelo usuário para TLS. 

Para obter mais informações sobre os recursos de segurança disponíveis no SQL Server, confira [Central de Segurança para o Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Próximas etapas

Para tarefas comuns de segurança, confira [Introdução aos recursos de segurança do SQL Server em Linux](sql-server-linux-security-get-started.md). Para que um script altere o número da porta TCP, os diretórios SQL Server e configure sinalizadores ou ordenação, confira [Configurar SQL Server em Linux com mssql-conf](sql-server-linux-configure-mssql-conf.md).
