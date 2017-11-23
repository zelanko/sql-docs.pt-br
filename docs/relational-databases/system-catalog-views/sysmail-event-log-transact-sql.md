---
title: sysmail_event_log (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aadbf36412f02f9a785d078d6fa949fcbeabc5f7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada mensagem do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornada pelo sistema Database Mail. (Mensagem neste contexto se refere a uma mensagem, como uma mensagem de erro, não uma mensagem de e-mail.) Configurar o **nível de log** parâmetro usando o **configurar parâmetros do sistema** caixa de diálogo do Assistente de configuração de email de banco de dados ou o [sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)procedimento armazenado, para determinar quais mensagens são retornadas.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|Identificador de itens no log.|  
|**event_type**|**varchar(11)**|O tipo de aviso inserido no log. Os valores possíveis são erros, avisos, mensagens informativas, mensagens de êxito e mensagens internas adicionais.|  
|**log_date**|**datetime**|A data e a hora em que a entrada de log foi feita.|  
|**Descrição**|**nvarchar(max)**|O texto da mensagem que está sendo registrada.|  
|**ID_do_processo**|**int**|O ID de processo do programa externo Database Mail. Isso normalmente é alterado toda vez que o programa externo Database Mail é iniciado.|  
|**mailitem_id**|**int**|Identificador do item de email na fila de email. NULL se a mensagem não estiver relacionada a um item de email específico.|  
|**account_id**|**int**|O **account_id** da conta referente ao evento. NULL se a mensagem não estiver relacionada a uma conta específica.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez. Para emails, este é o usuário que enviou o email. Para mensagens geradas pelo programa externo Database Mail, este é o contexto de usuário do programa.|  
  
## <a name="remarks"></a>Comentários  
 Ao solucionar problemas do Database Mail, pesquise o **sysmail_event_log** exibição para eventos relacionados a falhas de email. Algumas mensagens, como a falha do programa externo Database Mail, não estão associadas a emails específicos. Para procurar por erros relacionados a emails específicos, pesquisar o **mailitem_id** de email com falha no **sysmail_faileditems** exibir e, em seguida, procure o **sysmail_event_log**para mensagens relacionadas a esse **mailitem_id**. Quando um erro é retornado da **sp_send_dbmail**, o email não será enviado para o sistema de email de banco de dados e o erro não é exibido nessa exibição.  
  
 Quando houver falha em tentativas de entrega de conta individual, o Database Mail reterá as mensagens de erro durante tentativas de repetição até que a entrega do item de email obtenha êxito ou falhe. No caso de êxito final, todos os erros acumulados são registrados como avisos separados, incluindo o **account_id**. Isto pode causar o aparecimento de avisos, mesmo se o email foi enviado. Em caso de falha de entrega final, todos os avisos anteriores serão registrados como uma mensagem de erro sem um **account_id**, uma vez que todas as contas falharam.  
  
## <a name="permissions"></a>Permissões  
 Você deve ser um membro do **sysadmin** função de servidor fixa ou **DatabaseMailUserRole** função de banco de dados para acessar essa exibição. Membros de **DatabaseMailUserRole** que não são membros do **sysadmin** função, só poderá ver os eventos de emails que eles enviarem.  
  
## <a name="see-also"></a>Consulte também  
 [sysmail_faileditems &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Programa externo do Database Mail](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
