---
title: "Op&#231;&#227;o blocked process threshold de configura&#231;&#227;o de servidor | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "limites [SQL Server]"
  - "Opção blocked process threshold"
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Op&#231;&#227;o blocked process threshold de configura&#231;&#227;o de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use a opção **blocked process threshold** para especificar o limite, em segundos, no qual os relatórios de processo bloqueado serão gerados. O limite pode ser definido de 0 a 86.400. Por padrão, não são produzidos relatórios de processo bloqueado. Esse evento não é gerado para tarefas de sistema ou tarefas que estão esperando recursos que não geram deadlocks detectáveis.  
  
 É possível definir um [alerta](../../ssms/agent/alerts.md) a ser executado quando esse evento é gerado. Assim, por exemplo, é possível optar por chamar o administrador para tomar medidas adequadas a fim de resolver a situação de bloqueio.  
  
 O limite de processo bloqueado utiliza o thread em segundo plano do monitor deadlock para orientar a lista de tarefas que esperam por um tempo maior ou vários limites configurados. O evento é gerado uma vez por intervalo de relatório para cada uma das tarefas bloqueadas.  
  
 O relatório de processo bloqueado é feito em uma melhor base de esforço. Não há nenhuma garantia de qualquer relatório em tempo real ou até mesmo próximo a tempo real.  
  
 A configuração entra em vigor imediatamente, sem que o servidor seja parado e reiniciado.  
  
## Exemplos  
 O exemplo a seguir define o `blocked process threshold` em `20` segundos, gerando um relatório de processo bloqueado para cada tarefa que é bloqueada.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Classe de evento Blocked Process Report](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  