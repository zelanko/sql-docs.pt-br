---
description: sysmail_faileditems (Transact-SQL)
title: sysmail_faileditems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_faileditems
- sysmail_faileditems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_faileditems database mail view
ms.assetid: a31562c5-358e-4cfc-a72d-b3faccc53851
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 60e6e4b4411c55467aab30359ae25f07237ceb12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427888"
---
# <a name="sysmail_faileditems-transact-sql"></a>sysmail_faileditems (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada mensagem de Database Mail com o status de **falha** . Use esta exibição para determinar quais mensagens não foram enviadas com êxito.  
  
 Para ver todas as mensagens processadas por Database Mail, use [sysmail_allitems &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver apenas as mensagens não enviadas, use [sysmail_unsentitems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver apenas as mensagens que foram enviadas, use [sysmail_sentitems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md). Para exibir anexos de email, use [sysmail_mailattachments &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Identificador do item de email na fila de email.|  
|**profile_id**|**int**|O identificador do perfil usado para enviar a mensagem.|  
|**tiver**|**varchar(max)**|Os endereços de email dos destinatários da mensagem.|  
|**copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem.|  
|**blind_copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem, mas cujos nomes não aparecem no cabeçalho.|  
|**subject**|**nvarchar (510)**|A linha de assunto da mensagem.|  
|**body**|**varchar(max)**|O corpo da mensagem.|  
|**body_format**|**varchar (20)**|O formato do corpo da mensagem. Os valores possíveis são TEXT e HTML.|  
|**importance**|**varchar (6)**|O parâmetro de **importância** da mensagem.|  
|**prioridade**|**varchar (12)**|O parâmetro de **sensibilidade** da mensagem.|  
|**file_attachments**|**varchar(max)**|Uma lista delimitada por ponto-e-vírgula de nomes de arquivo anexados à mensagem de email.|  
|**Attachment_encoding**|**varchar (20)**|O tipo de anexo de email.|  
|**Consulta**|**varchar(max)**|A consulta executada pelo programa de email.|  
|**execute_query_database**|**sysname**|O contexto de banco de dados no qual o programa de email executou a consulta.|  
|**attach_query_result_as_file**|**bit**|Quando o valor é 0, os resultados da consulta são incluídos no corpo da mensagem de email, depois do conteúdo do corpo. Quando o valor é 1, os resultados são retornados como um anexo.|  
|**query_result_header**|**bit**|Quando o valor for 1, os resultados da consulta continham cabeçalhos de coluna. Quando o valor for 0, os resultados da consulta não incluirão cabeçalhos de coluna.|  
|**query_result_width**|**int**|O parâmetro **query_result_width** da mensagem.|  
|**query_result_separator**|**Char (1)**|O caractere usado para separar as colunas na saída da consulta.|  
|**exclude_query_output**|**bit**|O parâmetro **exclude_query_output** da mensagem. Para obter mais informações, consulte [sp_send_dbmail &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|O parâmetro **append_query_error** da mensagem. 0 indica que o Database Mail não deverá enviar a mensagem de email se houver um erro na consulta.|  
|**send_request_date**|**datetime**|A data e a hora em que a mensagem foi colocada na fila de email.|  
|**send_request_user**|**sysname**|O usuário que enviou a mensagem. Esse é o contexto de usuário do procedimento de email do banco de dados, e não o campo De da mensagem.|  
|**sent_account_id**|**int**|O identificador da conta do Database Mail usado para enviar a mensagem. Será sempre NULL para essa exibição.|  
|**sent_status**|**varchar (8)**|O status do email. Sempre **falhou** para esta exibição.|  
|**sent_date**|**datetime**|A data e a hora em que a mensagem foi removida da fila de email.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Comentários  
 Use a exibição **sysmail_faileditems** para ver quais mensagens não foram enviadas pelo Database Mail. Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando os atributos das mensagens que não foram enviadas. Para exibir o motivo da falha, consulte a entrada da mensagem com falha no modo de exibição [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) .  
  
## <a name="permissions"></a>Permissões  
 Concedida à função de servidor fixa **sysadmin** e à função de banco de dados **DatabaseMailUserRole** . Quando executado por um membro da função de servidor fixa **sysadmin** , essa exibição mostra todas as mensagens com falha. Todos os demais usuários veem somente as mensagens que falharam que eles submeteram.  
  
  
