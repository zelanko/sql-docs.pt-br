---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 44ab2e3106610f7b7130f997e9641e4aba685fd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127929"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>Exibições de Catálogo de Mensagens (para erros) – sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada **message_id** ou **Language_ID** das mensagens de erro no sistema, para as mensagens definidas pelo sistema e definidas pelo usuário. Para obter mais informações, veja [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|A identificação da mensagem. É exclusiva no servidor. As identificações de mensagem menores que 50000 são mensagens do sistema.|  
|**language_id**|**smallint**|ID de idioma para o qual o texto no **texto** é usado, conforme definido em **syslanguages**. Isso é exclusivo para um **message_id**especificado.|  
|**Severity**|**tinyint**|O nível de severidade da mensagem, entre 1 e 25. Isso é o mesmo para todos os idiomas de mensagem dentro de um **message_id**.|  
|**is_event_logged**|**bit**|1 = A mensagem mantém um log de evento quando surge um erro. Isso é o mesmo para todos os idiomas de mensagem dentro de um **message_id**.|  
|**text**|**nvarchar (2048)**|Texto da mensagem usada quando o **Language_ID** correspondente está ativo.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [LANÇAR &#40;&#41;Transact-SQL](../../t-sql/language-elements/throw-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mensagens &#40;para erros&#41; exibições de catálogo &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [Programação da caixa de mensagem de exceção](https://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [Mensagens de erro](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Eventos e erros do Mecanismo de Banco de Dados](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
