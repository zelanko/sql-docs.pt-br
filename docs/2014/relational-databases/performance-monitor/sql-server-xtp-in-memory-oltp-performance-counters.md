---
title: Contadores de desempenho de XTP (OLTP na memória) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69b24c96e4833a45038bfcae20f0a5fecd0d2340
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151132"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>Contadores de desempenho de XTP (OLTP na memória)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece objetos e contadores que podem ser usados pelo Monitor de Desempenho para monitorar a atividade OLTP in-memory.  
  
##  <a name="SQLServerPOs"></a> Objetos de desempenho XTP (OLTP na memória)  
 A tabela a seguir descreve objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de desempenho|Descrição|  
|------------------------|-----------------|  
|[Cursores de XTP](../cursors.md)|O objeto de desempenho Cursores de XTP contém os contadores relacionados aos cursores do mecanismo de XTP interno. Os cursores são os blocos de construção de baixo nível que o mecanismo de XTP usa para processar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] . Como tal, você normalmente não tem controle direto sobre eles.|  
|[Coleta de Lixo de XTP](sql-server-xtp-garbage-collection.md)|O objeto de desempenho Coleta de Lixo de XTP contém os contadores relacionados ao coletor de lixo do mecanismo de XTP.|  
|[Processador Fantasma de XTP](sql-server-xtp-phantom-processor.md)|O objeto de desempenho Processador Fantasma de XTP contém os contadores relacionados ao subsistema de processamento fantasma do mecanismo de XTP. Esse componente é responsável por detectar as linhas fantasmas nas transações que são executadas no nível de isolamento SERIALIZABLE.|  
|[Armazenamento de XTP](sql-server-xtp-storage.md)|O objeto de desempenho do Armazenamento de XTP contém os contadores relacionados ao Armazenamento de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Log de Transações de XTP](sql-server-xtp-transaction-log.md)|O objeto de desempenho Log de Transações de XTP contém os contadores relacionados ao log de transações de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Transações de XTP](sql-server-xtp-transactions.md)|O objeto de desempenho Transações de XTP contém os contadores relacionados às transações do mecanismo de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
