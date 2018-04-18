---
title: sysmail_faileditems (Transact-SQL) | Microsoft Docs
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
- sysmail_faileditems
- sysmail_faileditems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_faileditems database mail view
ms.assetid: a31562c5-358e-4cfc-a72d-b3faccc53851
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c156558b782eef8dc2ef76f06a012d3d6cd4967c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailfaileditems-transact-sql"></a>sysmail_faileditems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada mensagem de email de banco de dados com o **falha** status. Use esta exibição para determinar quais mensagens não foram enviadas com êxito.  
  
 Para ver todas as mensagens processadas pelo Database Mail, use [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver apenas as mensagens não enviadas, use [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver apenas as mensagens que foram enviadas, use [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md). Para exibir anexos de email, use [sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**Int**|Identificador do item de email na fila de email.|  
|**profile_id**|**Int**|O identificador do perfil usado para enviar a mensagem.|  
|**destinatários**|**varchar(max)**|Os endereços de email dos destinatários da mensagem.|  
|**copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem.|  
|**blind_copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem, mas cujos nomes não aparecem no cabeçalho.|  
|**subject**|**nvarchar(510)**|A linha de assunto da mensagem.|  
|**Corpo**|**varchar(max)**|O corpo da mensagem.|  
|**body_format**|**varchar(20)**|O formato do corpo da mensagem. Os valores possíveis são TEXT e HTML.|  
|**importance**|**varchar(6)**|O **importância** parâmetro da mensagem.|  
|**Sensibilidade**|**varchar(12)**|O **sensibilidade** parâmetro da mensagem.|  
|**file_attachments**|**varchar(max)**|Uma lista delimitada por ponto-e-vírgula de nomes de arquivo anexados à mensagem de email.|  
|**Attachment_encoding**|**varchar(20)**|O tipo de anexo de email.|  
|**Consulta**|**varchar(max)**|A consulta executada pelo programa de email.|  
|**execute_query_database**|**sysname**|O contexto de banco de dados no qual o programa de email executou a consulta.|  
|**attach_query_result_as_file**|**bit**|Quando o valor é 0, os resultados da consulta são incluídos no corpo da mensagem de email, depois do conteúdo do corpo. Quando o valor é 1, os resultados são retornados como um anexo.|  
|**query_result_header**|**bit**|Quando o valor for 1, os resultados da consulta continha cabeçalhos de coluna. Quando o valor for 0, resultados da consulta não incluem cabeçalhos de coluna.|  
|**query_result_width**|**Int**|O **query_result_width** parâmetro da mensagem.|  
|**query_result_separator**|**char(1)**|O caractere usado para separar as colunas na saída da consulta.|  
|**exclude_query_output**|**bit**|O **exclude_query_output** parâmetro da mensagem. Para obter mais informações, consulte [sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|O **append_query_error** parâmetro da mensagem. 0 indica que o Database Mail não deverá enviar a mensagem de email se houver um erro na consulta.|  
|**send_request_date**|**datetime**|A data e a hora em que a mensagem foi colocada na fila de email.|  
|**send_request_user**|**sysname**|O usuário que enviou a mensagem. Esse é o contexto de usuário do procedimento de email do banco de dados, e não o campo De da mensagem.|  
|**sent_account_id**|**Int**|O identificador da conta do Database Mail usado para enviar a mensagem. Será sempre NULL para essa exibição.|  
|**sent_status**|**varchar(8)**|O status do email. Sempre **falha** para esta exibição.|  
|**sent_date**|**datetime**|A data e a hora em que a mensagem foi removida da fila de email.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Remarks  
 Use o **sysmail_faileditems** exibição para ver quais mensagens não foram enviadas pelo Database Mail. Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando os atributos das mensagens que não foram enviadas. Para exibir o motivo da falha, consulte a entrada para a mensagem de falha de [sysmail_event_log &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) exibição.  
  
## <a name="permissions"></a>Permissões  
 Concedido a **sysadmin** função de servidor fixa e **databasemailuserrole** função de banco de dados. Quando executada por um membro de **sysadmin** função de servidor fixa, essa exibição mostra todas as falhas de mensagens. Todos os demais usuários veem somente as mensagens que falharam que eles submeteram.  
  
  
