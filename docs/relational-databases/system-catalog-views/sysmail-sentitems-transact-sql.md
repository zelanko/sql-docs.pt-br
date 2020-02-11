---
title: sysmail_sentitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_sentitems_TSQL
- sysmail_sentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_sentitems database mail view
ms.assetid: 16eb2a44-cebb-4cec-93ac-e2498c39989f
author: stevestein
ms.author: sstein
ms.openlocfilehash: c935a83c3c3fdd9fa577a3232e46caed7865c1c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70745363"
---
# <a name="sysmail_sentitems-transact-sql"></a>sysmail_sentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Contém uma linha para cada mensagem enviada pelo Database Mail. Use **sysmail_sentitems** quando desejar ver quais mensagens foram enviadas com êxito.  
  
 Para ver todas as mensagens processadas por Database Mail, use [sysmail_allitems &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver apenas as mensagens com o status de falha, use [sysmail_faileditems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver apenas as mensagens não enviadas ou repetidas, use [sysmail_unsentitems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver anexos de email, use [sysmail_mailattachments &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Identificador do item de email na fila de email.|  
|**profile_id**|**int**|O identificador do perfil usado para enviar a mensagem.|  
|**tiver**|**varchar(max)**|Os endereços de email dos destinatários da mensagem.|  
|**copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem.|  
|**blind_copy_recipients**|**varchar(max)**|Os endereços de email daqueles que recebem cópias da mensagem, mas cujos nomes não aparecem no cabeçalho.|  
|**Assunto**|**nvarchar (510)**|A linha de assunto da mensagem.|  
|**conteúdo**|**varchar(max)**|O corpo da mensagem.|  
|**body_format**|**varchar (20)**|O formato do corpo da mensagem. Os valores possíveis são **texto** e **HTML**.|  
|**porta**|**varchar (6)**|O parâmetro de **importância** da mensagem.|  
|**prioridade**|**varchar (12)**|O parâmetro de **sensibilidade** da mensagem.|  
|**file_attachments**|**varchar(max)**|Uma lista delimitada por ponto-e-vírgula de nomes de arquivo anexados à mensagem de email.|  
|**attachment_encoding**|**varchar (20)**|O tipo de anexo de email.|  
|**consultá**|**varchar(max)**|A consulta executada pelo programa de email.|  
|**execute_query_database**|**sysname**|O contexto de banco de dados no qual o programa de email executou a consulta.|  
|**attach_query_result_as_file**|**bit**|Quando o valor é 0, os resultados da consulta são incluídos no corpo da mensagem de email, depois do conteúdo do corpo. Quando o valor é 1, os resultados são retornados como um anexo.|  
|**query_result_header**|**bit**|Quando o valor for 1, os resultados da consulta continham cabeçalhos de coluna. Quando o valor for 0, os resultados da consulta não incluirão cabeçalhos de coluna.|  
|**query_result_width**|**int**|O parâmetro **query_result_width** da mensagem.|  
|**query_result_separator**|**char(1)**|O caractere usado para separar as colunas na saída da consulta.|  
|**exclude_query_output**|**bit**|O parâmetro **exclude_query_output** da mensagem. Para obter mais informações, consulte [sp_send_dbmail &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|O parâmetro **append_query_error** da mensagem. 0 indica que o Database Mail não deverá enviar a mensagem de email se houver um erro na consulta.|  
|**send_request_date**|**datetime**|A data e a hora em que a mensagem foi colocada na fila de email.|  
|**send_request_user**|**sysname**|O usuário que enviou a mensagem. Esse é o contexto de usuário do procedimento de email do banco de dados, e não o campo De da mensagem.|  
|**sent_account_id**|**int**|O identificador da conta do Database Mail usado para enviar a mensagem.|  
|**sent_status**|**varchar (8)**|O status do email. Sempre **enviado** para esta exibição.|  
|**sent_date**|**datetime**|A data e a hora em que a mensagem foi enviada.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Comentários  
 Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando os atributos das mensagens que foram enviadas com êxito. O Database Mail marca as mensagens como enviadas quando elas são submetidas com êxito a um servidor de email SMTP. Normalmente, o email é recebido em poucos minutos, mas o email pode ser atrasado devido a problemas com o servidor SMTP. O Database Mail marca a mensagem como enviada quando ela é aceita pelo servidor de email SMTP. Os erros de email ocorridos no servidor de email SMTP, tal como um endereço de email destinatário que não pode ser entregue, não são retornados ao Database Mail. Esses emails são registrados como enviados, embora não tenham sido entregues. Solucione o problema desse tipo de erro no servidor SMTP. Além disso, o servidor de email SMTP pode enviar uma notificação de mensagem que não pôde ser entregue para o endereço de email de resposta para uma conta do Database Mail.  
  
## <a name="permissions"></a>Permissões  
 Concedida à função de servidor fixa **sysadmin** e à função de banco de dados **DatabaseMailUserRole** . Quando executado por um membro da função de servidor fixa **sysadmin** , essa exibição mostra todas as mensagens enviadas. Todos os demais usuários veem somente as mensagens que eles enviaram.  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos do sistema de mensagens do Database Mail](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
  
