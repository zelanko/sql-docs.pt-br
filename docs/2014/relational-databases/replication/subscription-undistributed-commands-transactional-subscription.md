---
title: Assinatura, comandos não distribuídos (assinatura transacional, SQL Server 2005 e versões posterior) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a1f957c417c5c63766dfbffa923edd6935d1eb5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151488"
---
# <a name="subscription-undistributed-commands-transactional-subscription-sql-server-2005-and-later"></a>Assinatura, Comandos não Distribuídos (assinatura transacional, SQL Server 2005 e versões posteriores)
  A guia **Comandos não Distribuídos** exibe informações sobre o número de comandos no banco de dados de distribuição que não foram entregues ao Assinante selecionado, e, o tempo estimado para entrega desses comandos. Para obter informações sobre como exibir os comandos no banco de dados de distribuição, consulte [sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql).  
  
## <a name="options"></a>Opções  
 **Número de comandos no banco de dados de distribuição aguardando para serem aplicados a este Assinante**  
 O número de comandos no banco de dados de distribuição que não foram entregues ao Assinante selecionado. Um comando consiste em uma instrução DML (linguagem de manipulação de dados) ou uma instrução DDL (linguagem de definição de dados) Transact-SQL.  
  
 **Tempo estimado para aplicar esses comandos com base em desempenhos passados**  
 A quantidade de tempo estimada para entrega de comandos ao Assinante. Se esse valor for maior do que a quantidade de tempo requerida para gerar e aplicar um instantâneo ao Assinante, considere reiniciar o Assinante. Para obter mais informações, consulte [Reinicializar as assinaturas](reinitialize-subscriptions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)  
  
  
