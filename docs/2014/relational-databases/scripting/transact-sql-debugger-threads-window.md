---
title: Janela Threads | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.threads
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 91a2b7532792d5317114d269b77c036b86383592
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006791"
---
# <a name="threads-window"></a>Janela Threads
  A janela **Threads** exibe informações sobre o thread do [!INCLUDE[ssDE](../../includes/ssde-md.md)] usado antes da sessão do Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] que está sendo depurada. Você deve estar no modo de depuração para exibir as informações sobre thread.  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a janela Threads**  
  
-   No menu **Depurar** , clique em **Janelas**e em **Threads**.  
  
## <a name="columns"></a>Colunas  
 **ID**  
 É um número de identificação exclusiva que o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] atribui ao thread. Você pode localizar mais informações sobre o thread selecionando uma linha da exibição de gerenciamento dinâmico sys.dm_os_threads.  
  
 Se você não estiver executando em modo lightweight pooling, selecione a linha na qual o valor em os_thread_id corresponde ao valor da coluna **ID** . Se você estiver executando em modo lightweight pooling, selecione a linha na qual o valor em fiber_context_address corresponde ao valor na coluna **ID** .  
  
 **Nome**  
 Exibe informações sobre a sessão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no formato **ComputerName/InstanceName [SPID]**.  
  
 **ComputerName**  
 O nome do computador que está executando a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao qual a sessão do Editor de Consultas está conectada.  
  
 **InstanceName**  
 O nome da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] à qual a sessão do Editor de Consultas está conectada.  
  
 **[SPID]**  
 A sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processa a ID que identifica com exclusividade esta sessão. Você pode obter mais informações sobre a sessão selecionando a linha da exibição sys.sysprocesses que tem o mesmo valor na coluna spid.  
  
 **Local**  
 Exibe o nome do arquivo de script usado pela sessão em depuração do Editor de Consultas.  
  
 **Prioridade**  
 O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] não dá suporte a este recurso.  
  
 **Suspend**  
 O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] não dá suporte a este recurso.  
  
## <a name="see-also"></a>Consulte também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql)  
  
  
