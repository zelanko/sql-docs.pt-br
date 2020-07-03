---
title: sysmail_event_log (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68ef84e8efb3606042afbcf8579cf285a2077ab7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901047"
---
# <a name="sysmail_event_log-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada mensagem do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornada pelo sistema Database Mail. (A mensagem neste contexto refere-se a uma mensagem como uma mensagem de erro, não uma mensagem de email.) Configure o parâmetro de **nível de log** usando a caixa de diálogo **configurar parâmetros do sistema** do assistente de configuração do Database Mail ou o procedimento armazenado [sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md) para determinar quais mensagens são retornadas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|Identificador de itens no log.|  
|**event_type**|**varchar (11)**|O tipo de aviso inserido no log. Os valores possíveis são erros, avisos, mensagens informativas, mensagens de êxito e mensagens internas adicionais.|  
|**log_date**|**datetime**|A data e a hora em que a entrada de log foi feita.|  
|**ndescrição**|**nvarchar(max)**|O texto da mensagem que está sendo registrada.|  
|**process_id**|**int**|O ID de processo do programa externo Database Mail. Isso normalmente é alterado toda vez que o programa externo Database Mail é iniciado.|  
|**mailitem_id**|**int**|Identificador do item de email na fila de email. NULL se a mensagem não estiver relacionada a um item de email específico.|  
|**account_id**|**int**|A **account_id** da conta relacionada ao evento. NULL se a mensagem não estiver relacionada a uma conta específica.|  
|**last_mod_date**|**datetime**|A data e a hora da última modificação da linha.|  
|**last_mod_user**|**sysname**|O usuário que modificou a linha pela última vez. Para emails, este é o usuário que enviou o email. Para mensagens geradas pelo programa externo Database Mail, este é o contexto de usuário do programa.|  
  
## <a name="remarks"></a>Comentários  
 Ao solucionar problemas de Database Mail, pesquise o **sysmail_event_log** exibição para eventos relacionados a falhas de email. Algumas mensagens, como a falha do programa externo Database Mail, não estão associadas a emails específicos. Para procurar erros relacionados a emails específicos, procure a **mailitem_id** do email com falha na exibição **sysmail_faileditems** e, em seguida, pesquise o **sysmail_event_log** para encontrar mensagens relacionadas a esse **mailitem_id**. Quando um erro é retornado de **sp_send_dbmail**, o email não é enviado ao sistema Database Mail e o erro não é exibido nessa exibição.  
  
 Quando houver falha em tentativas de entrega de conta individual, o Database Mail reterá as mensagens de erro durante tentativas de repetição até que a entrega do item de email obtenha êxito ou falhe. No caso do sucesso final, todos os erros acumulados são registrados como avisos separados, incluindo o **account_id**. Isto pode causar o aparecimento de avisos, mesmo se o email foi enviado. No caso de falha de entrega final, todos os avisos anteriores são registrados como uma mensagem de erro sem um **account_id**, já que todas as contas falharam.  
  
## <a name="permissions"></a>Permissões  
 Você deve ser membro da função de servidor fixa **sysadmin** ou da função de banco de dados **DatabaseMailUserRole** para acessar essa exibição. Os membros de **DatabaseMailUserRole** que não são membros da função **sysadmin** só podem ver os eventos de emails que eles enviam.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sysmail_faileditems](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Programa externo do Database Mail](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
