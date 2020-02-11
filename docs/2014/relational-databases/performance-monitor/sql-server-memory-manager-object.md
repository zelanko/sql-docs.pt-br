---
title: SQL Server, objeto Gerenciador de Memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Manager
- Memory Manager object
ms.assetid: dbf49000-eeb0-4e9c-a361-5092363920dc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 822cb494b7dce35ea965a2a53cab36785a38bc75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250624"
---
# <a name="sql-server-memory-manager-object"></a>SQL Server, objeto Memory Manager
  O objeto **Gerenciador de memória** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft fornece contadores para monitorar o uso geral da memória do servidor. Monitorar o uso de memória de servidor global para medir a atividade de usuário e uso de recursos pode ajudá-lo a identificar gargalos de desempenho. Monitorar a memória usada por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ajudar a determinar:  
  
-   Se existem gargalos a partir de memória física inadequada para o armazenamento de dados frequentemente acessados em cache. Se a memória estiver inadequada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] terá que recuperar os dados do disco.  
  
-   Se o desempenho das consultas pode ser melhorado pela adição de memória ou pela disponibilização de mais memória para o cache de dados ou para as estruturas internas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="memory-manager-counters"></a>Contadores do Gerenciador de Memória  
 Essa tabela descreve os contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Gerenciador de Memória** .  
  
|Contadores do Gerenciador de Memória do SQL Server|DESCRIÇÃO|  
|----------------------------------------|-----------------|  
|**Memória de conexão (KB)**|Especifica a quantidade total de memória dinâmica que o servidor está usando para manter conexões.|  
|**Memória cache do banco de dados (KB)**|Especifica a quantidade de memória que o servidor está usando atualmente para o cache de páginas de banco de dados.|  
|**Memória livre (KB)**|Especifica a quantidade de memória comprometida que não está atualmente em uso pelo servidor.|  
|**Memória de espaço de trabalho concedida (KB)**|Especifica a quantidade total de memória concedida atualmente para a execução de processos, como hash, classificação, cópia em massa e operações de criação de índice.|  
|**Blocos de bloqueio**|Especifica o número atual de blocos de bloqueio em uso no servidor (atualizado periodicamente). Um bloco de bloqueio representa um recurso individual bloqueado, como uma tabela, página ou linha.|  
|**Blocos de bloqueio alocados**|Especifica o número atual de blocos de bloqueio alocados. Na inicialização do servidor, o número de blocos de bloqueio alocados mais o número de blocos de proprietário de bloqueio alocados dependem da opção de configuração [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **do** . Se forem necessários mais blocos de bloqueio, o valor aumentará.|  
|**Memória de bloqueio (KB)**|Especifica a quantidade total de memória dinâmica que o servidor está usando para os bloqueios.|  
|**Blocos de proprietário de bloqueio**|Especifica o número de blocos de proprietário de bloqueio atualmente em uso no servidor (atualizado periodicamente). Um bloco de proprietário de bloqueio representa a propriedade de um bloqueio em um objeto por um thread individual. Portanto, se três threads tiverem, cada um, um bloqueio compartilhado (S) em uma página, haverá três blocos de proprietário de bloqueio.|  
|**Blocos de proprietário de bloqueio alocados**|Especifica o número atual de blocos de proprietário de bloqueio alocados. Na inicialização do servidor, o número de blocos de proprietário de bloqueio alocados e o número de blocos de bloqueio alocados dependem da opção de configuração [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **do** . Se forem necessários mais blocos de proprietário de bloqueio, o valor aumentará dinamicamente.|  
|**Memória máxima do espaço de trabalho (KB)**|Indica a quantidade máxima de memória disponível para a execução de processos, como hash, classificação, cópia em massa e operações de criação de índice.|  
|**Concessões de memória pendentes**|Especifica o número total de processos que adquiriram com êxito uma concessão de memória de workspace.|  
|**Concessões de memória pendente**|Especifica o número total de processos que estão aguardando por uma concessão de memória de workspace.|  
|**Memória do otimizador (KB)**|Especifica a quantidade total de memória dinâmica que o servidor está usando para a otimização de consultas.|  
|**Memória reservada do servidor (KB)**|Indica a quantidade de memória que o servidor reservou para uso futuro. Esse contador exibe a quantidade atual de memória não usada inicialmente concedida que é mostrada em **Memória de Workspace Concedida (KB)**.|  
|**Memória cache do SQL (KB)**|Especifica a quantidade total de memória dinâmica que o servidor está usando para o cache de SQL dinâmico.|  
|**Memória de servidor roubada (KB)**|Especifica a quantidade de memória que o servidor está usando para outras finalidades que não sejam páginas de banco de dados.|  
|**Memória do servidor de destino (KB)**|Indica a quantidade ideal de memória que o servidor pode consumir.|  
|**Memória total do servidor (KB)**|Especifica a quantidade de memória que o servidor comprometeu usando o gerenciador de memória.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, objeto Gerenciador de buffer](sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
