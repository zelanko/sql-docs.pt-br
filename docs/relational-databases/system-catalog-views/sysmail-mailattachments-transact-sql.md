---
title: sysmail_mailattachments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c263f7e3df69b6eb3d9517b2dc973a1cb4102f7d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627304"
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada anexo enviado ao Database Mail. Use esta exibição quando quiser informações sobre anexos do Database Mail. Para examinar todos os emails processados pelo Database Mail, use [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|Identificador do anexo.|  
|**mailitem_id**|**int**|Identificador do item de email que continha o anexo.|  
|**filename**|**nvarchar(520)**|O nome de arquivo do anexo. Quando **attach_query_result** é 1 e **query_attachment_filename** for NULL, o Database Mail cria um nome de arquivo arbitrário.|  
|**filesize**|**int**|O tamanho do anexo em bytes.|  
|**attachment**|**varbinary(max)**|O conteúdo do anexo.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Comentários  
 Ao solucionar problemas do Database Mail, use esta exibição para ver as propriedades dos anexos.  
  
 Anexos armazenados nas tabelas do sistema podem fazer com que o **msdb** banco de dados cresça. Use **sysmail_delete_mailitems_sp** para excluir itens de email e seus anexos. Para obter mais informações, consulte [criar um trabalho do SQL Server Agent para arquivar mensagens do Database Mail e Logs de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permissões  
 Concedido para o **sysadmin** função de servidor fixa e a **DatabaseMailUserRole** função de banco de dados. Quando executada por um membro dos **sysadmin** função de servidor fixa, essa exibição mostra todos os anexos. Todos os outros usuários veem somente os anexos de mensagens que enviaram.  
  
## <a name="see-also"></a>Consulte também  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
