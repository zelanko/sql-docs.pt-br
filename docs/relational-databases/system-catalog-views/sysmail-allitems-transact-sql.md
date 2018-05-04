---
title: sysmail_allitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sysmail_allitems_TSQL
- sysmail_allitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_allitems database mail view
ms.assetid: 21fb8432-7677-4435-902f-64a58bba4cbb
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26eb86ab6228c4b9e1439993c94a0cac15f6b880
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailallitems-transact-sql"></a>sysmail_allitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada mensagem processada pelo Database Mail. Use esta exibição para consultar o status de todas as mensagens.  
  
 Para ver somente as mensagens com o status de falha, use [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver apenas as mensagens não enviadas, use [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver apenas as mensagens que foram enviadas, use [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
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
|**attachment_encoding**|**varchar(20)**|O tipo de anexo de email.|  
|**query**|**varchar(max)**|A consulta executada pelo programa de email.|  
|**execute_query_database**|**sysname**|O contexto de banco de dados no qual o programa de email executou a consulta.|  
|**attach_query_result_as_file**|**bit**|Quando o valor é 0, os resultados da consulta são incluídos no corpo da mensagem de email, depois do conteúdo do corpo. Quando o valor é 1, os resultados são retornados como um anexo.|  
|**query_result_header**|**bit**|Quando o valor for 1, os resultados da consulta continha cabeçalhos de coluna. Quando o valor for 0, resultados da consulta não incluem cabeçalhos de coluna.|  
|**query_result_width**|**Int**|O **query_result_width** parâmetro da mensagem.|  
|**query_result_separator**|**char(1)**|O caractere usado para separar as colunas na saída da consulta.|  
|**exclude_query_output**|**bit**|O **exclude_query_output** parâmetro da mensagem. Para obter mais informações, consulte [sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|O **append_query_error** parâmetro da mensagem. 0 indica que o Database Mail não deverá enviar a mensagem de email se houver um erro na consulta.|  
|**send_request_date**|**datetime**|A data e a hora em que a mensagem foi colocada na fila de email.|  
|**send_request_user**|**sysname**|O usuário que enviou a mensagem. Esse é o contexto de usuário do procedimento de email do banco de dados, e não o campo De da mensagem.|  
|**sent_account_id**|**Int**|O identificador da conta do Database Mail usado para enviar a mensagem.|  
|**sent_status**|**varchar(8)**|O status do email. Os valores possíveis são:<br /><br /> **enviado** -o email foi enviado.<br /><br /> **não enviado** -o Database mail ainda está tentando enviar a mensagem.<br /><br /> **repetindo** -Database Mail não conseguiu enviar a mensagem, mas está tentando enviá-la novamente.<br /><br /> **Falha** -o Database mail não conseguiu enviar a mensagem.|  
|**sent_date**|**datetime**|A data e a hora em que a mensagem foi enviada.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Remarks  
 Use o **sysmail_allitems** exibição para ver o status de todas as mensagens processadas pelo Database Mail. Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando os atributos das mensagens que foram enviadas comparados aos atributos das mensagens que não foram enviadas.  
  
 As tabelas do sistema expostas por esta exibição contêm todas as mensagens e pode causar a **msdb** banco de dados cresça. Exclua periodicamente da exibição as mensagens antigas para reduzir o tamanho das tabelas. Para obter mais informações, consulte [criar um trabalho do SQL Server Agent para arquivar mensagens de email de banco de dados e Logs de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permissões  
 Concedido a **sysadmin** função de servidor fixa e **DatabaseMailUserRole** função de banco de dados. Quando executada por um membro de **sysadmin** função de servidor fixa, essa exibição mostra todas as mensagens. Todos os demais usuários veem somente as mensagens que eles submeteram.  
  
  
