---
title: Contadores de desempenho de XTP (OLTP na memória) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b12c482300ff8908236d1eda9d0e030df4b2e356
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116574"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>Contadores de desempenho de XTP (OLTP na memória)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece objetos e contadores que podem ser usados pelo Monitor de Desempenho para monitorar a atividade OLTP in-memory.  
  
##  <a name="SQLServerPOs"></a> Objetos de desempenho XTP (OLTP na memória)  
 A tabela a seguir descreve objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de desempenho|Description|  
|------------------------|-----------------|  
|[Cursores de XTP](../cursors.md)|O objeto de desempenho Cursores de XTP contém os contadores relacionados aos cursores do mecanismo de XTP interno. Os cursores são os blocos de construção de baixo nível que o mecanismo de XTP usa para processar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] . Como tal, você normalmente não tem controle direto sobre eles.|  
|[Coleta de Lixo de XTP](sql-server-xtp-garbage-collection.md)|O objeto de desempenho Coleta de Lixo de XTP contém os contadores relacionados ao coletor de lixo do mecanismo de XTP.|  
|[Processador Fantasma de XTP](sql-server-xtp-phantom-processor.md)|O objeto de desempenho Processador Fantasma de XTP contém os contadores relacionados ao subsistema de processamento fantasma do mecanismo de XTP. Esse componente é responsável por detectar as linhas fantasmas nas transações que são executadas no nível de isolamento SERIALIZABLE.|  
|[Armazenamento de XTP](sql-server-xtp-storage.md)|O objeto de desempenho do Armazenamento de XTP contém os contadores relacionados ao Armazenamento de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Log de Transações de XTP](sql-server-xtp-transaction-log.md)|O objeto de desempenho Log de Transações de XTP contém os contadores relacionados ao log de transações de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Transações de XTP](sql-server-xtp-transactions.md)|O objeto de desempenho Transações de XTP contém os contadores relacionados às transações do mecanismo de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  