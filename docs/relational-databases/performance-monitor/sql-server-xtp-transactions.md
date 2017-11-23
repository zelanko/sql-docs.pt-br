---
title: "Transações XTP do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33f78f5c77854ca6d4a324e4df07d68276511a7b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-xtp-transactions"></a>Transações XTP do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto de desempenho do Log Transações XTP do SQL Server contém contadores relacionados às transações que envolvem OLTP in-memory no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores **Transações de XTP do SQL Server** .  
  
|Contador|Descrição|  
|-------------|-----------------|  
|**Anulações em cascata/s**|O número de transações que foram revertidas devido a uma reversão de dependência de confirmação (em média), por segundo.|  
|**Dependências de confirmação realizadas/s**|O número de dependências de confirmação realizadas por transações (em média), por segundo.|  
|**Transações somente leitura preparadas/s**|O número de transações somente leitura que foram preparadas para o processamento da confirmação, por segundo.|  
|**Atualizações de ponto de salvamento/s**|O número de vezes que um ponto de salvamento foi “atualizado”, (em média), por segundo. Uma atualização de ponto de salvamento é quando um ponto de salvamento existente é redefinido para o momento atual no tempo de vida da transação.|  
|**Reversões de ponto de salvamento/s**|O número de vezes que uma transação foi revertida para um ponto de salvamento (em média), por segundo.|  
|**Pontos de salvamento criados/s**|O número de pontos de salvamento criados (em média), por segundo.|  
|**Falha de validação de transação/s**|O número de transações que falharam no processamento de validação (em média), por segundo.|  
|**Transações anuladas por usuário/s**|O número de transações que foram anuladas pelo usuário (em média), por segundo.|  
|**Transações anuladas/s**|O número de transações que foram anuladas (pelo usuário e pelo sistema) em média, por segundo.|  
|**Transações criadas/s**|O número de transações criadas no sistema (em média), por segundo.<br /><br /> As transações de XTP são contadas diferentemente de transações baseadas em disco (conforme refletido em bancos de dados:transações/s). Por exemplo, transações criadas/s contam como transações somente leitura, mas isso não ocorre com bancos de dados:transações/s.|  
  
## <a name="see-also"></a>Consulte também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
