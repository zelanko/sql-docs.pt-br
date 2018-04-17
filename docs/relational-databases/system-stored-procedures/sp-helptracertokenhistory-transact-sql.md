---
title: sp_helptracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1763672f446560e06686c46af3cc060045500ed8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações de latência detalhada por tokens de rastreamento especificados, com uma linha retornada para cada Assinante. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação na qual o token de rastreamento foi inserido. *publicação* é **sysname**, sem padrão.  
  
 [  **@tracer_id=** ] *tracer_id*  
 É a ID do token de rastreamento no [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabela para o histórico de quais informações são retornadas. *tracer_id* é **int**, sem padrão.  
  
 [  **@publisher=** ] **'***publicador***'**  
 O nome do publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro só deve ser especificado para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 O nome do banco de dados de publicação. *publisher_db* é **sysname**, com um valor padrão de NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|Número de segundos entre o registro de token de rastreamento sendo aplicado no Publicador e o registro sendo aplicado no Distribuidor.|  
|**Assinante**|**sysname**|Nome do Assinante que recebeu o token de rastreamento.|  
|**subscriber_db**|**sysname**|Nome do banco de dados de assinatura no qual o registro de token de rastreamento foi inserido.|  
|**subscriber_latency**|**bigint**|Número de segundos entre o registro de token de rastreamento aplicado no Distribuidor e o registro aplicado no Assinante.|  
|**overall_latency**|**bigint**|Número de segundos entre o registro de token de rastreamento aplicado no Publicador e o registro de token aplicado no Assinante.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helptracertokenhistory** é usado em replicação transacional.  
  
 Executar [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) para obter uma lista de tokens de rastreamento para a publicação.  
  
 Um valor NULL no conjunto de resultados significa que não podem ser calculadas estatísticas de latência. Isso porque o token de rastreamento não foi recebido no Distribuidor ou em um dos Assinantes.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa, o **db_owner** função de banco de dados fixa no banco de dados de publicação, ou **db_owner** banco de dados fixo ou  **replmonitor** funções no banco de dados de distribuição podem executar **sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Consulte também  
 [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
