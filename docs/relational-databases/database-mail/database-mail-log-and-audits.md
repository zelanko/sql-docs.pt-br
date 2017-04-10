---
title: "Registro em log e auditoria do Database Mail | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "auditando [SQL Server]"
  - "Database Mail [SQL Server], auditando"
  - "logs [Database Mail]"
  - "auditorias [SQL Server], Database Mail"
  - "Database Mail [SQL Server], registro em log"
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
caps.latest.revision: 30
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 30
---
# Registro em log e auditoria do Database Mail
  A funcionalidade de log do Database Mail é criada para fornecer um modo de isolar e corrigir problemas. O Database Mail armazena as informações de log no banco de dados **msdb** . Informações sobre conteúdo de e-mail do Database Mail, status de emails e qualquer mensagem recebida, tais como erros, são registradas em log pelo Database Mail e podem ser usadas para fins de solução de problemas e auditoria.  
  
## Logs do Database Mail  
 Tabelas no banco de dados **msdb** registram informações do [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md). [Exibições do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md) expõe as tabelas para fins de solução de problemas. Erros aparecem na exibição [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) quando o Service Broker não consegue ativar o programa externo, se o programa externo encontra erros de rede ou se o servidor SMTP recusa uma mensagem de email. Na eventualidade de o programa externo não conseguir fazer registros nas tabelas do **msdb** , o programa registrará os erros no log de eventos de aplicativos do Windows.  
  
 Tabelas internas do **msdb** contêm as mensagens de email e anexos enviados por meio do Database Mail, além do status atual de cada mensagem. O Database Mail atualiza essas tabelas assim que cada mensagem é processada.  
  
## Tarefas de auditoria do Database Mail  
  
|||  
|-|-|  
|**Examinando e gerenciando logs do Database Mail**|**Link para tópico**|  
|Verifique o status de entrega de uma mensagem individual|[Verificar o status de mensagens de email enviadas por Database Mail](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|Limpe mensagens, anexos e entradas de log do Database Mail|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|Arquive mensagens e logs do Database Email|[Criar um trabalho do SQL Server Agent para arquivar mensagens do Database Mail e logs de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  