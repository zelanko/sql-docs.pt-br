---
title: sys. messages (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac13b8d68accd744803b7524f9d6d179cca0446b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032429"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>Exibições do catálogo de mensagens (para erros) – sys. messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada **message_id** ou **language_id** das mensagens de erro no sistema, para mensagens tanto definida pelo sistema e definidas pelo usuário. Para obter mais informações, veja [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|A identificação da mensagem. É exclusiva no servidor. As identificações de mensagem menores que 50000 são mensagens do sistema.|  
|**language_id**|**smallint**|ID de idioma para o qual o texto no **texto** for usado, conforme definido na **syslanguages**. Isso é exclusivo para determinado **message_id**.|  
|**severity**|**tinyint**|O nível de severidade da mensagem, entre 1 e 25. Isso é o mesmo para todos os idiomas de mensagem em uma **message_id**.|  
|**is_event_logged**|**bit**|1 = A mensagem mantém um log de evento quando surge um erro. Isso é o mesmo para todos os idiomas de mensagem em uma **message_id**.|  
|**text**|**nvarchar(2048)**|Texto da mensagem usado quando correspondente **language_id** está ativa.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mensagens de &#40;erros&#41; exibições do catálogo &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [Mensagem de exceção programação da caixa](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [Mensagens de erro](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Eventos e erros do Mecanismo de Banco de Dados](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
