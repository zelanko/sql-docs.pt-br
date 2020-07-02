---
title: sp_posttracertoken (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0f5bc0b6e7960faac9d68469750c445e469896e1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720214"
---
# <a name="sp_posttracertoken-transact-sql"></a>sp_posttracertoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Esse procedimento envia um token de rastreamento para um log de transações no Publicador e inicia o processo de rastreamento de estatística de latência. As informações são registradas quando o token de rastreamento é gravado no log de transações, quando é captado pelo Agente de Leitor de Log e quando é aplicado pelo Agente de Distribuição. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Para obter mais informações, consulte [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_posttracertoken [ @publication = ] 'publication'   
    [ , [ @tracer_token_id = ] tracer_token_id OUTPUT  
    [ , [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação para a qual a latência está sendo medida. a *publicação* é **sysname**, sem padrão.  
  
`[ @tracer_token_id = ] _tracer_token_id OUTPUT`É a ID do token de rastreamento inserido. *tracer_token_id* é **int** com um padrão de NULL e é um parâmetro de saída. Esse valor pode ser usado para executar [sp_helptracertokenhistory &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md) ou [sp_deletetracertokenhistory &#40;Transact-SQL](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)&#41;sem primeiro executar [sp_helptracertokens &#40;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md).  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL e não deve ser especificado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_posttracertoken** é usado na replicação transacional.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_posttracertoken**.  
  
## <a name="see-also"></a>Consulte Também  
 [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
