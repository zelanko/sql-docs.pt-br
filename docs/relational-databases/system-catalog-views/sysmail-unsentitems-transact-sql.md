---
title: sysmail_unsentitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
author: stevestein
ms.author: sstein
ms.openlocfilehash: f84e84ed7801beb20bdaca5c92d333133fad3b63
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70745354"
---
# <a name="sysmail_unsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Contém uma linha para cada Database Mail mensagem com o status não **enviado** ou **repetido** . As mensagens com status unsent ou retrying ainda estão na fila de email e podem ser enviadas a qualquer momento. As mensagens podem ter o status não **enviado** pelos seguintes motivos:  
  
-   A mensagem é nova e foi colocada na fila de email, mas o Database Mail está cuidando de outras mensagens e ainda não a alcançou.  
  
-   O programa externo do Database Mail não está em execução e nenhum email está sendo enviado.  
  
 As mensagens podem ter o status de **nova tentativa** pelos seguintes motivos:  
  
-   O Database Mail tentou enviar o email, mas o servidor de email SMTP não pôde ser contatado. O Database Mail continuará a tentar enviar a mensagem usando outras contas do Database Mail atribuídas ao perfil que enviou a mensagem. Se nenhuma conta puder enviar o email, Database Mail aguardará o período de tempo configurado para o parâmetro de **atraso de repetição de conta** e tentará enviar a mensagem novamente. Database Mail usa o parâmetro de **tentativas de repetição de conta** para determinar quantas vezes tentar enviar a mensagem. As mensagens retêm o status de **repetição** , contanto que Database Mail esteja tentando enviar a mensagem.  
  
 Use essa exibição para saber quantas mensagens estão aguardando o envio e há quanto tempo estão na fila de email. Normalmente, o número de mensagens não **enviadas** será baixo. Faça um teste de parâmetro durante as operações normais para determinar um número razoável de mensagens que devam ficar na fila para suas operações.  
  
 Para ver todas as mensagens processadas por Database Mail, use [sysmail_allitems &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver apenas as mensagens com o status de falha, use [sysmail_faileditems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver apenas as mensagens que foram enviadas, use [sysmail_sentitems &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
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
|**send_request_user**|**sysname**|O usuário que enviou a mensagem. Este é o contexto de usuário do procedimento do Database Mail, não o campo **de** da mensagem.|  
|**sent_account_id**|**int**|O identificador da conta do Database Mail usado para enviar a mensagem. Será sempre NULL para essa exibição.|  
|**sent_status**|**varchar (8)**|Não será **enviado** se Database Mail não tiver tentado enviar o email. Estará **tentando** novamente se Database Mail falha ao enviar a mensagem, mas está tentando novamente.|  
|**sent_date**|**datetime**|A data e a hora em que o Database Mail tentou enviar o email pela última vez. Será NULL se o Database Mail não tentar enviar a mensagem.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez.|  
  
## <a name="remarks"></a>Comentários  
 Na solução de problemas do Database Mail, essa exibição pode ajudá-lo a identificar a natureza do problema, mostrando o número de mensagens a serem enviadas e há quanto tempo estão aguardando o envio. Se nenhuma mensagem for enviada, talvez o programa externo do Database Mail não esteja funcionando ou haja um problema de rede impedindo que ele entre em contato com os servidores SMTP. Se muitas das mensagens não enviadas tiverem o mesmo **profile_id**, poderá haver um problema com o servidor SMTP. Considere a opção de adicionar outras contas ao perfil. Se as mensagens forem enviadas, mas estiverem aguardando muito tempo na fila, talvez sejam necessários mais recursos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processar o volume requisitado de mensagens.  
  
## <a name="permissions"></a>Permissões  
 Concedida à função de servidor fixa **sysadmin** e à função de banco de dados **DatabaseMailUserRole** . Quando executado por um membro da função de servidor fixa **sysadmin** , essa exibição mostra todas as mensagens não **enviadas** ou **repetidas** . Todos os outros usuários veem apenas as mensagens não **enviadas** ou **repetidas** que eles enviaram.  
  
  
