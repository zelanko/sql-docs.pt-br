---
description: sysmail_allitems (Transact-SQL)
title: sysmail_allitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_allitems_TSQL
- sysmail_allitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_allitems database mail view
ms.assetid: 21fb8432-7677-4435-902f-64a58bba4cbb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0c5a41e6f0c150638eeed8e1c7cdd4fbb3c6bf2b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419910"
---
# <a name="sysmail_allitems-transact-sql"></a>sysmail_allitems (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Contém uma linha para cada mensagem processada pelo Database Mail. Use esta exibição para consultar o status de todas as mensagens.  
  
 Para ver apenas as mensagens com o status de falha, use [sysmail_faileditems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver apenas as mensagens não enviadas, use [sysmail_unsentitems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver apenas as mensagens que foram enviadas, use [sysmail_sentitems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
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
|**attachment_encoding**|**varchar (20)**|O tipo de anexo de email.|  
|**consulta**|**varchar(max)**|A consulta executada pelo programa de email.|  
|**execute_query_database**|**sysname**|O contexto de banco de dados no qual o programa de email executou a consulta.|  
|**attach_query_result_as_file**|**bit**|Quando o valor é 0, os resultados da consulta são incluídos no corpo da mensagem de email, depois do conteúdo do corpo. Quando o valor é 1, os resultados são retornados como um anexo.|  
|**query_result_header**|**bit**|Quando o valor for 1, os resultados da consulta continham cabeçalhos de coluna. Quando o valor for 0, os resultados da consulta não incluirão cabeçalhos de coluna.|  
|**query_result_width**|**int**|O parâmetro **query_result_width** da mensagem.|  
|**query_result_separator**|**Char (1)**|O caractere usado para separar as colunas na saída da consulta.|  
|**exclude_query_output**|**bit**|O parâmetro **exclude_query_output** da mensagem. Para obter mais informações, consulte [sp_send_dbmail &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|O parâmetro **append_query_error** da mensagem. 0 indica que o Database Mail não deverá enviar a mensagem de email se houver um erro na consulta.|  
|**send_request_date**|**datetime**|A data e a hora em que a mensagem foi colocada na fila de email.|  
|**send_request_user**|**sysname**|O usuário que enviou a mensagem. Esse é o contexto de usuário do procedimento de email do banco de dados, e não o campo De da mensagem.|  
|**sent_account_id**|**int**|O identificador da conta do Database Mail usado para enviar a mensagem.|  
|**sent_status**|**varchar (8)**|O status do email. Os valores possíveis são:<br /><br /> **enviado** -o email foi enviado.<br /><br /> Não **enviado** -o Database Mail ainda está tentando enviar a mensagem.<br /><br /> a **repetição** de-Database Mail falhou ao enviar a mensagem, mas está tentando enviá-la novamente.<br /><br /> **falha** -o Database Mail não pôde enviar a mensagem.|  
|**sent_date**|**datetime**|A data e a hora em que a mensagem foi enviada.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Comentários  
 Use a exibição **sysmail_allitems** para ver o status de todas as mensagens processadas pelo Database Mail. Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando os atributos das mensagens que foram enviadas comparados aos atributos das mensagens que não foram enviadas.  
  
 As tabelas do sistema expostas por essa exibição contêm todas as mensagens e podem fazer com que o banco de dados **msdb** cresça. Exclua periodicamente da exibição as mensagens antigas para reduzir o tamanho das tabelas. Para obter mais informações, consulte [criar um trabalho de SQL Server Agent para arquivar Database Mail mensagens e logs de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permissões  
 Concedida à função de servidor fixa **sysadmin** e à função de banco de dados **DatabaseMailUserRole** . Quando executado por um membro da função de servidor fixa **sysadmin** , essa exibição mostra todas as mensagens. Todos os demais usuários veem somente as mensagens que eles submeteram.  
  
  
