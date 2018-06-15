---
title: sysmail_sentitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_sentitems_TSQL
- sysmail_sentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_sentitems database mail view
ms.assetid: 16eb2a44-cebb-4cec-93ac-e2498c39989f
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de4547bec20880375fc29fc746588983b2ec9d2e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33222077"
---
# <a name="sysmailsentitems-transact-sql"></a>sysmail_sentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada mensagem enviada pelo Database Mail. Use **sysmail_sentitems** quando desejar ver quais mensagens foram enviadas com êxito.  
  
 Para ver todas as mensagens processadas pelo Database Mail, use [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver somente as mensagens com o status de falha, use [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver apenas não enviadas ou repetir mensagens, use [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver os anexos de email, use [sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**Int**|Identificador do item de email na fila de email.|  
|**profile_id**|**Int**|O identificador do perfil usado para enviar a mensagem.|  
|**destinatários**|**varchar(max)**|Os endereços de email dos destinatários da mensagem.|  
|**copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem.|  
|**blind_copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem, mas cujos nomes não aparecem no cabeçalho.|  
|**subject**|**nvarchar(510)**|A linha de assunto da mensagem.|  
|**Corpo**|**varchar(max)**|O corpo da mensagem.|  
|**body_format**|**varchar(20)**|O formato do corpo da mensagem. Os valores possíveis são **texto** e **HTML**.|  
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
|**sent_status**|**varchar(8)**|O status do email. Sempre **enviados** para esta exibição.|  
|**sent_date**|**datetime**|A data e a hora em que a mensagem foi enviada.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Remarks  
 Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando os atributos das mensagens que foram enviadas com êxito. O Database Mail marca as mensagens como enviadas quando elas são submetidas com êxito a um servidor de email SMTP. Normalmente, o email é recebido em poucos minutos, mas o email pode ser atrasado devido a problemas com o servidor SMTP. O Database Mail marca a mensagem como enviada quando ela é aceita pelo servidor de email SMTP. Os erros de email ocorridos no servidor de email SMTP, tal como um endereço de email destinatário que não pode ser entregue, não são retornados ao Database Mail. Esses emails são registrados como enviados, embora não tenham sido entregues. Solucione o problema desse tipo de erro no servidor SMTP. Além disso, o servidor de email SMTP pode enviar uma notificação de mensagem que não pôde ser entregue para o endereço de email de resposta para uma conta do Database Mail.  
  
## <a name="permissions"></a>Permissões  
 Concedido a **sysadmin** função de servidor fixa e **databasemailuserrole** função de banco de dados. Quando executada por um membro de **sysadmin** função de servidor fixa, essa exibição mostra todas as mensagens enviadas. Todos os demais usuários veem somente as mensagens que eles enviaram.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos do sistema de mensagens do Database Mail](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
  
