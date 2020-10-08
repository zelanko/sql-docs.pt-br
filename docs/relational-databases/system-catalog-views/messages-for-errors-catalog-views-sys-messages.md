---
description: Exibições de Catálogo de Mensagens (para erros) – sys.messages
title: sys. Messages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 30cfb208d709f19743216369b23e6b7bef9dfc38
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810392"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>Exibições de Catálogo de Mensagens (para erros) – sys.messages
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada **message_id** ou **Language_ID** das mensagens de erro no sistema, para as mensagens definidas pelo sistema e definidas pelo usuário. Para obter mais informações, veja [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|A identificação da mensagem. É exclusiva no servidor. As identificações de mensagem menores que 50000 são mensagens do sistema.|  
|**language_id**|**smallint**|ID de idioma para o qual o texto no **texto** é usado, conforme definido em **syslanguages**. Isso é exclusivo para um **message_id**especificado.|  
|**severity**|**tinyint**|O nível de severidade da mensagem, entre 1 e 25. Isso é o mesmo para todos os idiomas de mensagem dentro de um **message_id**.|  
|**is_event_logged**|**bit**|1 = A mensagem mantém um log de evento quando surge um erro. Isso é o mesmo para todos os idiomas de mensagem dentro de um **message_id**.|  
|**text**|**nvarchar(2048)**|Texto da mensagem usada quando o **Language_ID** correspondente está ativo.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mensagens &#40;para erros&#41; exibições de catálogo &#40;Transact-SQL&#41;]()   
 [Programação da caixa de mensagem de exceção](/previous-versions/sql/sql-server-2016/ms166343(v=sql.130))   
 [Mensagens de erro](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Eventos e erros do Mecanismo de Banco de Dados](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
