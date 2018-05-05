---
title: sp_dropdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6a0e47c9fc680895cacc0c2e68585a354391b98f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um trabalho de instantâneo de dados filtrado para uma publicação com filtros de linha com parâmetros. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Quando o trabalho é excluído, todos os dados relacionados são excluídos do [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) tabela do sistema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação da qual o trabalho de instantâneo de dados filtrados está sendo removido. *publicação* é **sysname**, sem padrão.  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 É o nome do trabalho do instantâneo de dados filtrado que está sendo removido. *dynamic_snapshot_jobname*é sysname, e se não for fornecido, será padronizado para qualquer trabalho nome é associado ao *dynamic_snapshot_jobid*.  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 É um identificador do trabalho de instantâneo de dados filtrado que está sendo removido. *dynamic_snapshot_jobid*é **uniqueidentifier**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Somente *dynamic_snapshot_jobid*ou *dynamic_snapshot_jobname* pode ser especificado. Se não forem fornecidos valores para um *dynamic_snapshot_jobid*ou *dynamic_snapshot_jobname*, todos os trabalhos de instantâneo dinâmico para a publicação são removidos.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 *ignore_distributor* é **bit**, com um padrão de **0**. Esse parâmetro pode ser usado para descartar um trabalho de instantâneo dinâmico sem realizar tarefas de limpeza no Distribuidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropdynamicsnapshot** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_dropdynamicsnapshot**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_adddynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
