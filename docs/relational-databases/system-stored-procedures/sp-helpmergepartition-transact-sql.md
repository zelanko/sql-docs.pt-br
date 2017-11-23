---
title: sp_helpmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords: sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2c4e931f2da9794392056595ab71b88e005a26f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergepartition-transact-sql"></a>sp_helpmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações de partição para a publicação de mesclagem especificada. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@suser_sname=** ] **'***suser_sname***'**  
 É o valor de SUSER_SNAME usado para definir uma partição. *suser_sname* é **sysname**, com um valor padrão de NULL. Forneça esse parâmetro para limitar o conjunto de resultados só a partições onde SUSER_SNAME resolve para o valor fornecido.  
  
> [!NOTE]  
>  Quando *suser_sname* for fornecido, *host_name* deve ser NULL  
  
 [  **@host_name=** ] **'***host_name***'**  
 É o valor de HOST_NAME usado para definir uma partição. *HOST_NAME* é **sysname**, com um valor padrão de NULL. Forneça esse parâmetro para limitar o conjunto de resultados só a partições onde HOST_NAME resolve para o valor fornecido.  
  
> [!NOTE]  
>  Quando *suser_sname* for fornecido, *host_name* deve ser NULL  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**partição**|**int**|Identifica a partição do Assinante.|  
|**HOST_NAME**|**sysname**|Valor usado ao criar a partição para uma assinatura filtrada pelo valor da [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) função no assinante.|  
|**suser_sname**|**sysname**|Valor usado ao criar a partição para uma assinatura filtrada pelo valor da [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) função no assinante.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Local do instantâneo de dados filtrado para a partição do Assinante.|  
|**date_refreshed**|**datetime**|Último data em que o trabalho de instantâneo foi executado para gerar o instantâneo de dados filtrado para a partição.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifica o trabalho que cria o instantâneo de dados filtrado para uma partição.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergepartition** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor e o **db_owner** pode executar a função de banco de dados fixa **sp_helpmergepartition**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addmergepartition &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_dropmergepartition &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
