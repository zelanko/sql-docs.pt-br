---
title: Banco de Dados em Memória | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory database
- feature, in-memory database
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: d61ea85f5c1d7784faaf1d094e2fa858bffcd8c2
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255410"
---
# <a name="in-memory-database"></a>Banco de dados em memória

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Banco de Dados em Memória é um termo abrangente para os recursos do SQL Server que aproveitam tecnologias baseadas em memória. Conforme novos recursos baseados em memória são desenvolvidos, esta página continuará sendo atualizada.

## <a name="hybrid-buffer-pool"></a>Pool de Buffers Híbrido

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [Pool de Buffers Híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md) permite que o mecanismo de banco de dados acesse diretamente as páginas de dados em arquivos de banco de dados armazenados em dispositivos PMEM (Memória Persistente).

## <a name="memory-optimized-tempdb-metadata"></a>Metadados do TempDB com otimização de memória

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] apresenta um novo recurso, que são os [metadados do tempdb com otimização de memória](./databases/tempdb-database.md#memory-optimized-tempdb-metadata), que remove efetivamente alguns gargalos de contenção e possibilita um novo nível de escalabilidade para cargas de trabalho com uso intenso do tempdb.

## <a name="in-memory-oltp"></a>OLTP na memória

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [OLTP in-memory](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) é a principal tecnologia disponível no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e no [!INCLUDE[ssSDS](../includes/sssds-md.md)] para otimizar o desempenho do processamento de transações, a ingestão de dados, o carregamento de dados e cenários de dados transitórios.

**Aplica-se a:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

## <a name="persistent-memory-support-for-linux"></a>Suporte de memória persistente para Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

O [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] adiciona suporte para dispositivos PMEM (Memória Persistente) ao Linux, fornecendo capacitação completa de arquivos de log de transações e dados colocados na [memória persistente](../linux/sql-server-linux-configure-pmem.md).

**Aplica-se a:** [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
