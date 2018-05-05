---
title: sysmail_mailattachments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d4d4e5088f0ec91fc8de28b1c82886b7bc26419
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada anexo enviado ao Database Mail. Use esta exibição quando quiser informações sobre anexos do Database Mail. Para examinar todos os emails processados pelo Database Mail, use [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**Int**|Identificador do anexo.|  
|**mailitem_id**|**Int**|Identificador do item de email que continha o anexo.|  
|**filename**|**nvarchar(520)**|O nome de arquivo do anexo. Quando **attach_query_result** é 1 e **query_attachment_filename** for NULL, o Database Mail cria um nome de arquivo arbitrário.|  
|**filesize**|**Int**|O tamanho do anexo em bytes.|  
|**attachment**|**varbinary(max)**|O conteúdo do anexo.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Remarks  
 Ao solucionar problemas do Database Mail, use esta exibição para ver as propriedades dos anexos.  
  
 Os anexos armazenados nas tabelas do sistema podem causar a **msdb** banco de dados cresça. Use **sysmail_delete_mailitems_sp** para excluir itens de email e seus anexos. Para obter mais informações, consulte [criar um trabalho do SQL Server Agent para arquivar mensagens de email de banco de dados e Logs de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permissões  
 Concedido para o **sysadmin** função fixa de servidor e o **DatabaseMailUserRole** função de banco de dados. Quando executada por um membro de **sysadmin** função de servidor fixa, essa exibição mostra todos os anexos. Todos os outros usuários veem somente os anexos de mensagens que enviaram.  
  
## <a name="see-also"></a>Consulte também  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
