---
title: Coleta de lixo de OLTP in-memory | Microsoft Docs
description: Saiba mais sobre a coleta de lixo no OLTP in-memory no SQL Server. Se uma transação que não está mais ativa excluir uma linha, ela estará sujeita à coleta de lixo.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 940140a7-4785-46fc-8bf4-151435dccd3c
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed9bc2a1d7791c593ab33335aea2967411117bac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723144"
---
# <a name="in-memory-oltp-garbage-collection"></a>Coleta de lixo de OLTP na memória
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Uma linha de dados é considerada obsoleta se foi excluída por uma transação que não está mais ativa. Uma linha obsoleta é qualificada para a coleta de lixo. Estas são características da coleta de lixo no [!INCLUDE[hek_2](../../includes/hek-2-md.md)]:  
  
-   Sem bloqueio. A coleta de lixo é distribuída com o tempo com um impacto mínimo sobre a carga de trabalho.  
  
-   Cooperativa. As transações de usuário participam da coleta de lixo com o thread principal de coleta de lixo.  
  
-   Eficiente. Transações de usuário desvinculam linhas obsoletas no caminho de acesso (o índice) em uso. Isso reduz o trabalho necessário quando a linha é finalmente removida.  
  
-   Respondendo. A pressão da memória leva à coleta de lixo agressiva.  
  
-   Escalonável. Após a confirmação, transações de usuário fazem parte do trabalho de coleta de lixo. Quanto maior for a atividade transacional, mais transações existirão para desvincular linhas obsoletas.  
  
 A coleta de lixo é controlada pelo thread principal de coleta de lixo. O thread principal de coleta de lixo é executado a cada minuto, ou quando o número de transações confirmadas excede um limite interno. A tarefa do coletor de lixo é:  
  
-   Identificar as transações que excluíram ou atualizaram um conjunto de linhas e que foram confirmadas antes da transação ativa mais antiga.  
  
-   Identificar versões de linha criadas por essas transações antigas.  
  
-   Agrupar as linhas antigas em uma ou mais unidades de 16 linhas cada. Isso é feito para distribuir o trabalho do coletor de lixo em unidades menores.  
  
-   Mover essas unidades de trabalho para a fila de coleta de lixo, uma para cada agendador. Consulte esses DMVs do coletor de lixo para obter os detalhes: [sys.dm_xtp_gc_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md), [sys.dm_db_xtp_gc_cycle_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md) e [sys.dm_xtp_gc_queue_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md).  
  
 Após a confirmação de uma transação de usuário, ele identifica todos os itens enfileirados associados ao agendador que ele executou e libera a memória. Se a fila de coleta de lixo no agendador estiver vazia, ele procurará uma fila não vazia no nó NUMA atual. Se houver baixa atividade transacional e pressão de memória, o thread principal da coleta de lixo poderá acessar linhas da coleta de lixo de qualquer fila. Se não houver atividade transacional (por exemplo) após a exclusão de um grande número de linhas e não houver pressão de memória, as linhas excluídas não passarão por coleta de lixo até a atividade transacional ser retomada ou haver pressão de memória.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando memória para OLTP in-memory](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)  
  
  
