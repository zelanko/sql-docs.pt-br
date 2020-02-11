---
title: SQL Server, objeto Bloqueios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Locks object
- SQLServer:Locks
ms.assetid: ace04f0d-3993-4444-8317-ca39d7087e49
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cd7773177f6ec9d02df9d3d669abf561919ffe0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250609"
---
# <a name="sql-server-locks-object"></a>SQL Server, objeto Locks
  O objeto **SqlServer: Locks** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft fornece informações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre bloqueios em tipos de recursos individuais. Os bloqueios são mantidos nos recursos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como linhas lidas ou modificadas durante uma transação, para evitar o uso simultâneo de recursos por transações diferentes. Por exemplo, se um bloqueio exclusivo (X) for mantido em uma linha de uma tabela por uma transação, nenhuma outra transação poderá modificar essa linha até que o bloqueio seja liberado. Minimizar bloqueios aumenta a simultaneidade, o que pode melhorar o desempenho. Várias instâncias do objeto **Locks** podem ser monitoradas ao mesmo tempo, com cada instância representando um bloqueio em um tipo de recurso.  
  
 Esta tabela descreve os contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** .  
  
|Contadores Locks do SQL Server|DESCRIÇÃO|  
|-------------------------------|-----------------|  
|**Tempo de espera médio (MS)**|Tempo médio de espera (em milissegundos) de cada solicitação de bloqueio que resultou em uma espera.|  
|**Solicitações de bloqueio/s**|Número de bloqueios novos e conversões de bloqueio, por segundo, solicitados a partir do gerenciador de bloqueios.|  
|**Tempos limite de bloqueio (tempo limite > 0)/s**|Número de solicitações de bloqueio, por segundo, que ultrapassaram o tempo limite, excluindo-se solicitações de bloqueios NOWAIT.|  
|**Tempos limite de bloqueio/s**|Número de solicitações de bloqueio, por segundo, que ultrapassaram o tempo limite, inclusive solicitações de bloqueios NOWAIT.|  
|**Tempo de espera de bloqueio (MS)**|Tempo de espera total (em milissegundos) dos bloqueios no último segundo.|  
|**Esperas de bloqueio/s**|Número de solicitações de bloqueio, por segundo, que exigiram que o chamador esperasse.|  
|**Número de deadlocks/s**|Número de solicitações de bloqueio, por segundo, que resultaram em um deadlock.|  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode bloquear esses recursos.  
  
|Item|DESCRIÇÃO|  
|----------|-----------------|  
|**_Total**|Informações de todos os bloqueios.|  
|**AllocUnit**|Um bloqueio em uma unidade de alocação.|  
|**Aplicativo**|Um bloqueio em um recurso especificado por aplicativo.|  
|**Backup de banco de dados**|Um bloqueio em um banco de dados, inclusive todos os seus objetos.|  
|**Tention**|Um bloqueio em um grupo contíguo de 8 páginas.|  
|**Arquivo**|Um bloqueio em um arquivo de banco de dados.|  
|**Heap/árvore b**|Heap ou BTree (HOBT). Um bloqueio em um heap de páginas de dados ou na estrutura BTree de um índice.|  
|**Chave**|Um bloqueio em uma linha de um índice.|  
|**Metadados**|Um bloqueio em uma parte das informações de catálogo, também chamadas de metadados.|  
|**Objeto**|Um bloqueio em tabela, procedimento armazenado, exibição, etc, inclusive todos os dados e índices. O objeto pode ser qualquer coisa que tenha uma entrada em **sys.all_objects**.|  
|**Página**|Um bloqueio em uma página de 8 quilobytes (KB) em um banco de dados.|  
|**ELIMINÁ**|ID de linha. Um bloqueio em uma única linha de um heap.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
