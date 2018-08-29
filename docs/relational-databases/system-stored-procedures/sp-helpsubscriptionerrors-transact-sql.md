---
title: sp_helpsubscriptionerrors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpsubscriptionerrors_TSQL
- sp_helpsubscriptionerrors
helpviewer_keywords:
- sp_helpsubscriptionerrors
ms.assetid: 01c8bc21-939e-490d-8cc8-219c068be31e
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 870e8197a8182ab813ea8b165b46b4888f96726e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031959"
---
# <a name="sphelpsubscriptionerrors-transact-sql"></a>sp_helpsubscriptionerrors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna todos os erros de replicação transacionais para uma determinada assinatura. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsubscriptionerrors [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**, sem padrão.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* está **sysname**, sem padrão.  
  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@subscriber=** ] **'***assinante***'**  
 É o nome do Assinante. *assinante* está **sysname**, sem padrão.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* está **sysname**, sem padrão.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do erro.|  
|**time**|**datetime**|Hora em que o erro ocorreu.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|ID do tipo de origem do erro.|  
|**source_name**|**nvarchar(100)**|Nome de origem do erro.|  
|**error_code**|**sysname**|Código do erro.|  
|**error_text**|**ntext**|Mensagem de erro.|  
|**xact_seqno**|**varbinary(16)**|Número de sequência do log de transações iniciais do lote de execução com falha. Usado somente por Distribution Agents, esse é o número de sequência do log de transações da primeira transação do lote de execução com falha.|  
|**command_id**|**int**|ID do comando do lote de execução com falha. Usado somente por Distribution Agents, essa é a ID de comando do primeiro comando do lote de execução com falha.|  
|**session_id**|**int**|ID da sessão do agente na qual ocorreu o erro.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpsubscriptionerrors** é usado com o instantâneo e replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_helpsubscriptionerrors**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
