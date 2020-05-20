---
title: sp_dropdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0c9f33c4f50f77ed8ded47b6d7f69a2476f49227
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830146"
---
# <a name="sp_dropdynamicsnapshot_job-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um trabalho de instantâneo de dados filtrado para uma publicação com filtros de linha com parâmetros. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Quando o trabalho é excluído, todos os dados relacionados são excluídos da tabela do sistema [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação da qual o trabalho de instantâneo de dados filtrado está sendo removido. a *publicação* é **sysname**, sem padrão.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`É o nome do trabalho de instantâneo de dados filtrado que está sendo removido. *dynamic_snapshot_jobname*é sysname e, se não for fornecido, o padrão será qualquer nome de trabalho associado a *dynamic_snapshot_jobid*.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`É um identificador para o trabalho de instantâneo de dados filtrado que está sendo removido. *dynamic_snapshot_jobid*é **uniqueidentifier**, com o padrão NULL.  
  
> [!IMPORTANT]  
>  Somente *dynamic_snapshot_jobid*ou *dynamic_snapshot_jobname* podem ser especificados. Se os valores não forem fornecidos para *dynamic_snapshot_jobid*ou *dynamic_snapshot_jobname*, todos os trabalhos de instantâneo dinâmico para a publicação serão removidos.  
  
`[ @ignore_distributor = ] ignore_distributor`*ignore_distributor* é **bit**, com um padrão de **0**. Esse parâmetro pode ser usado para descartar um trabalho de instantâneo dinâmico sem realizar tarefas de limpeza no Distribuidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropdynamicsnapshot** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_dropdynamicsnapshot**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
