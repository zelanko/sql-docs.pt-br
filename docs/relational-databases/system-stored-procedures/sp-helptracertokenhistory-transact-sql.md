---
title: sp_helptracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 36809be121087741d2a23becf41a32b2ffe9f5cd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826027"
---
# <a name="sp_helptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações de latência detalhada por tokens de rastreamento especificados, com uma linha retornada para cada Assinante. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação na qual o token de rastreamento foi inserido. a *publicação* é **sysname**, sem padrão.  
  
`[ @tracer_id = ] tracer_id`É a ID do token de rastreamento no [MStracer_tokens &#40;tabela de&#41;Transact-SQL](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) para a qual as informações de histórico são retornadas. *tracer_id* é **int**, sem padrão.  
  
`[ @publisher = ] 'publisher'`O nome do Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]
>  Esse parâmetro só deve ser especificado para não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.  
  
`[ @publisher_db = ] 'publisher_db'`O nome do banco de dados de publicação. *publisher_db* é **sysname**, com um valor padrão de NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|Número de segundos entre o registro de token de rastreamento sendo aplicado no Publicador e o registro sendo aplicado no Distribuidor.|  
|**farão**|**sysname**|Nome do Assinante que recebeu o token de rastreamento.|  
|**subscriber_db**|**sysname**|Nome do banco de dados de assinatura no qual o registro de token de rastreamento foi inserido.|  
|**subscriber_latency**|**bigint**|Número de segundos entre o registro de token de rastreamento aplicado no Distribuidor e o registro aplicado no Assinante.|  
|**overall_latency**|**bigint**|Número de segundos entre o registro de token de rastreamento aplicado no Publicador e o registro de token aplicado no Assinante.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helptracertokenhistory** é usado na replicação transacional.  
  
 Execute [sp_helptracertokens &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) para obter uma lista de tokens de rastreamento para a publicação.  
  
 Um valor NULL no conjunto de resultados significa que não podem ser calculadas estatísticas de latência. Isso porque o token de rastreamento não foi recebido no Distribuidor ou em um dos Assinantes.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** no banco de dados de publicação ou **db_owner** banco de dados fixo ou funções **replmonitor** no banco de dados de distribuição podem executar **sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Consulte Também  
 [Medir a latência e validar conexões para replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [&#41;&#40;Transact-SQL de sp_deletetracertokenhistory](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
