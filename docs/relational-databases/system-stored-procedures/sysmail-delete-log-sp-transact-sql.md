---
title: sysmail_delete_log_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_delete_log_sp_TSQL
- sysmail_delete_log_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_delete_log_sp
ms.assetid: e94b37a1-70ad-46a5-86c0-721892156f7c
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d479d84bda33ff7b1ef2877f0d783f9588d84e4a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysmaildeletelogsp-transact-sql"></a>sysmail_delete_log_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui eventos do log do Database Mail. Exclui todos os eventos no log ou os eventos que atendem a critérios de data ou de tipo.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@logged_before**  =] **'***logged_before***'**  
 Exclui entradas até a data e hora especificadas pelo *logged_before* argumento. *logged_before* é **datetime** com NULL como padrão. NULL indica todas as datas.  
  
 [  **@event_type**  =] **'***event_type***'**  
 Exclui entradas de log de tipo especificado como o *event_type*. *event_type* é **varchar(15)** sem nenhum padrão. As entradas válidas são **êxito**, **aviso**, **erro**, e **informativa**. NULL indica todos os tipos de evento.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Use o **sysmail_delete_log_sp** procedimento armazenado para excluir permanentemente as entradas do log do Database Mail. Um argumento opcional permite excluir somente os registros mais antigos fornecendo uma data e hora. Os eventos mais antigos que o argumento serão excluídos. Um argumento opcional permite excluir somente os eventos de um determinado tipo, especificado como o **event_type** argumento.  
  
 A exclusão de entradas no log do Database Mail não exclui as entradas de emails das tabelas do Database Mail. Use [sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) para excluir email das tabelas do Database Mail.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa pode acessar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-deleting-all-events"></a>A. Excluindo todos os eventos  
 O exemplo a seguir exclui todos os eventos no log do Database Mail.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>B. Excluindo os eventos mais antigos  
 O exemplo a seguir exclui os eventos no log do Database Mail anteriores a 9 de outubro de 2005.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>C. Excluindo todos os eventos de um determinado tipo  
 O exemplo a seguir exclui todas as mensagens de êxito no log do Database Mail.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sysmail_event_log &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_delete_mailitems_sp &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [Criar um trabalho do SQL Server Agent para arquivar mensagens e logs de eventos do Database Mail](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
