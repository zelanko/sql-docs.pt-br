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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0fd6122ec99d4f5788fbe9f2b33478df7723f238
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900970"
---
# <a name="sysmail_mailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada anexo enviado ao Database Mail. Use esta exibição quando quiser informações sobre anexos do Database Mail. Para examinar todos os emails processados por Database Mail use [sysmail_allitems &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|Identificador do anexo.|  
|**mailitem_id**|**int**|Identificador do item de email que continha o anexo.|  
|**nome do arquivo**|**nvarchar (520)**|O nome de arquivo do anexo. Quando **attach_query_result** é 1 e **query_attachment_filename** é nulo, Database Mail cria um nome de arquivo arbitrário.|  
|**tamanho**|**int**|O tamanho do anexo em bytes.|  
|**Associação**|**varbinary(max)**|O conteúdo do anexo.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Comentários  
 Ao solucionar problemas do Database Mail, use esta exibição para ver as propriedades dos anexos.  
  
 Os anexos armazenados nas tabelas do sistema podem fazer com que o banco de dados **msdb** cresça. Use **sysmail_delete_mailitems_sp** para excluir itens de email e seus anexos associados. Para obter mais informações, consulte [criar um trabalho de SQL Server Agent para arquivar Database Mail mensagens e logs de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permissões  
 Concedido à função de servidor fixa **sysadmin** e à função de banco de dados **DatabaseMailUserRole** . Quando executado por um membro da função de servidor fixa **sysadmin** , essa exibição mostra todos os anexos. Todos os outros usuários veem somente os anexos de mensagens que enviaram.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sysmail_allitems](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_faileditems](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_sentitems](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_unsentitems](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
