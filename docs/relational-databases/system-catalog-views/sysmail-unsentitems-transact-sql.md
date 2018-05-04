---
title: sysmail_unsentitems (Transact-SQL) | Microsoft Docs
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
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8e67548b6e561e8c9cf06a552bef743f25f59886
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailunsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada mensagem de email de banco de dados com o **unsent** ou **repetindo** status. As mensagens com status unsent ou retrying ainda estão na fila de email e podem ser enviadas a qualquer momento. As mensagens podem ter o **unsent** status pelos seguintes motivos:  
  
-   A mensagem é nova e foi colocada na fila de email, mas o Database Mail está cuidando de outras mensagens e ainda não a alcançou.  
  
-   O programa externo do Database Mail não está em execução e nenhum email está sendo enviado.  
  
 As mensagens podem ter o **repetindo** status pelos seguintes motivos:  
  
-   O Database Mail tentou enviar o email, mas o servidor de email SMTP não pôde ser contatado. O Database Mail continuará a tentar enviar a mensagem usando outras contas do Database Mail atribuídas ao perfil que enviou a mensagem. Se nenhuma conta puder enviar o email, o Database Mail aguardará o período de tempo configurado para o **atraso na repetição de conta** parâmetro e, em seguida, tentar enviar a mensagem novamente. Database Mail usa o **tentativas de repetição de conta** parâmetro para determinar quantas vezes tentará enviar a mensagem. As mensagens manterão **repetindo** , desde que o Database Mail está tentando enviar a mensagem de status.  
  
 Use essa exibição para saber quantas mensagens estão aguardando o envio e há quanto tempo estão na fila de email. Normalmente, o número de **unsent** mensagens será baixas. Faça um teste de parâmetro durante as operações normais para determinar um número razoável de mensagens que devam ficar na fila para suas operações.  
  
 Para ver todas as mensagens processadas pelo Database Mail, use [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver somente as mensagens com o status de falha, use [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver apenas as mensagens que foram enviadas, use [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
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
|**send_request_user**|**sysname**|O usuário que enviou a mensagem. Este é o contexto de usuário do procedimento de email de banco de dados, não o **de** campo da mensagem.|  
|**sent_account_id**|**Int**|O identificador da conta do Database Mail usado para enviar a mensagem. Será sempre NULL para essa exibição.|  
|**sent_status**|**varchar(8)**|Será **unsent** se o Database Mail não tentar enviar o email. Será **repetindo** se o Database Mail não conseguiu enviar a mensagem, mas tentar novamente.|  
|**sent_date**|**datetime**|A data e a hora em que o Database Mail tentou enviar o email pela última vez. Será NULL se o Database Mail não tentar enviar a mensagem.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Remarks  
 Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando o número de mensagens a serem enviadas e há quanto tempo estão aguardando o envio. Se nenhuma mensagem for enviada, talvez o programa externo do Database Mail não esteja funcionando ou haja um problema de rede impedindo que ele entre em contato com os servidores SMTP. Se muitas mensagens não enviadas tiverem o mesmo **profile_id**, pode haver um problema com o servidor SMTP. Considere a opção de adicionar outras contas ao perfil. Se as mensagens forem enviadas, mas estiverem aguardando muito tempo na fila, talvez sejam necessários mais recursos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processar o volume requisitado de mensagens.  
  
## <a name="permissions"></a>Permissões  
 Concedido a **sysadmin** função de servidor fixa e **DatabaseMailUserRole** função de banco de dados. Quando executada por um membro do **sysadmin** função de servidor fixa, essa exibição mostra todos os **unsent** ou **repetindo** mensagens. Todos os demais usuários veem somente o **unsent** ou **repetindo** mensagens que eles submeteram.  
  
  
