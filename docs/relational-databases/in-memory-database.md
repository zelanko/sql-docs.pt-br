---
title: Recursos e tecnologias de sistemas de banco de dados em memória
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory systems
- in-memory technologies
- in-memory features
- database, in-memory database
- system, in-memory system
- features, in-memory features
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
ms.openlocfilehash: 0c71bda5a459c7993de824cdb6665978ba57166f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892463"
---
# <a name="in-memory-database-systems-and-technologies"></a>Tecnologias e sistemas de banco de dados em memória

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

Esta página destina-se a servir como uma página de referência para recursos e tecnologias em memória no SQL Server. O conceito de um sistema de banco de dados em memória refere-se a um sistema de banco de dados que foi projetado para aproveitar capacidades de memória maiores disponíveis em sistemas de banco de dados modernos. Um banco de dados em memória pode ser relacional ou não relacional por natureza.

Frequentemente assume-se que as vantagens de desempenho de um sistema de banco de dados em memória se devem principalmente ao fato de ele ser mais rápido para acessar os dados residentes na memória em vez de os dados localizados até mesmo nos subsistemas de discos mais rápido disponíveis (por várias ordens de magnitude). No entanto, muitas cargas de trabalho do SQL Server podem se ajustar a todo o conjunto de trabalho na memória disponível. Muitos sistemas de banco de dados em memória podem persistir dados em disco e nem sempre podem ser capazes de se ajustar a todo o conjunto de dados na memória disponível.

Um cache volátil rápido que traz uma mídia consideravelmente mais lenta, mas durável, era predominante para cargas de trabalho de banco de dados relacional. Ele precisa de abordagens específicas para o gerenciamento de carga de trabalho. As oportunidades apresentadas por taxas de transferência de memória mais rápidas, maior capacidade ou até mesmo a memória persistente facilitam o desenvolvimento de novos recursos e tecnologias que podem estimular novas abordagens ao gerenciamento de carga de trabalho de banco de dados relacional.

## <a name="hybrid-buffer-pool"></a>Pool de buffers híbrido

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

[O pool de buffers híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md) expande o pool de buffers para arquivos de banco de dados que residem em dispositivos de armazenamento de memória persistente endereçáveis por byte para plataformas Windows e Linux com [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="memory-optimized-tempdb-metadata"></a>Metadados `tempdb` com otimização de memória

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] apresenta um novo recurso, que são os [metadados do tempdb com otimização de memória](./databases/tempdb-database.md#memory-optimized-tempdb-metadata), que remove efetivamente alguns gargalos de contenção e possibilita um novo nível de escalabilidade para cargas de trabalho com uso intenso do tempdb.

## <a name="in-memory-oltp"></a>OLTP na memória

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

O [OLTP in-memory](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) é uma tecnologia de banco de dados disponível no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e no [!INCLUDE[ssSDS](../includes/sssds-md.md)] para otimizar o desempenho do processamento de transações, a ingestão de dados, o carregamento de dados e cenários de dados transitórios.

## <a name="configuring-persistent-memory-support-for-linux"></a>Configurando o suporte de memória persistente para Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] descreve como configurar a memória persistente (PMEM) usando o utilitário `ndctl` de [memória persistente](../linux/sql-server-linux-configure-pmem.md).

## <a name="persisted-log-buffer"></a>Buffer de log persistente

O Service Pack 1 de [!INCLUDE[ssSQL16](../includes/sssql16-md.md)] introduziu uma otimização de desempenho para cargas de trabalho com uso intensivo de gravação que foram associadas por esperas de WRITELOG. A memória persistente é usada para armazenar o buffer de log. Esse buffer, que é pequeno (20 MB por banco de dados de usuário), deve ser liberado para o disco para que as transações gravadas no log de transações sejam protegidas. Para cargas de trabalho OLTP com uso intensivo de gravação, esse mecanismo de liberação pode se tornar um gargalo. Com o buffer de log na memória persistente, o número de operações necessárias para proteger o log é reduzido, aprimorando os tempos de transação gerais e aumentando o desempenho da carga de trabalho. Esse processo foi introduzido como [Final do cache de log]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/). No entanto, houve um conflito percebido com [Backups de log de transações final](./backup-restore/tail-log-backups-sql-server.md) e o entendimento tradicional de que a parte final do log foi a porção do log de transações protegida, mas ainda não foi feito backup. Como o nome do recurso oficial é um buffer de log persistente, esse é o nome usado aqui.

Confira [Adicionar buffer de log persistente a um banco de dados](./databases/add-persisted-log-buffer.md).
