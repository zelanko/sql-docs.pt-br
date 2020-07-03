---
title: sp_helpmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 276e1a886a999858585533ee35b6c5f3cf109657
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881526"
---
# <a name="sp_helpmergepartition-transact-sql"></a>sp_helpmergepartition (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna as informações de partição para a publicação de mesclagem especificada. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @suser_sname = ] 'suser_sname'`É o valor SUSER_SNAME usado para definir uma partição. *SUSER_SNAME* é **sysname**, com um valor padrão de NULL. Forneça esse parâmetro para limitar o conjunto de resultados só a partições onde SUSER_SNAME resolve para o valor fornecido.  
  
> [!NOTE]  
>  Quando *SUSER_SNAME* é fornecido, *HOST_NAME* deve ser nulo  
  
`[ @host_name = ] 'host_name'`É o valor HOST_NAME usado para definir uma partição. *HOST_NAME* é **sysname**, com um valor padrão de NULL. Forneça esse parâmetro para limitar o conjunto de resultados só a partições onde HOST_NAME resolve para o valor fornecido.  
  
> [!NOTE]  
>  Quando *SUSER_SNAME* é fornecido, *HOST_NAME* deve ser nulo  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**particion**|**int**|Identifica a partição do Assinante.|  
|**host_name**|**sysname**|Valor usado ao criar a partição para uma assinatura que é filtrada pelo valor da função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) no Assinante.|  
|**suser_sname**|**sysname**|Valor usado ao criar a partição para uma assinatura que é filtrada pelo valor da função [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) no Assinante.|  
|**dynamic_snapshot_location**|**nvarchar (255)**|Local do instantâneo de dados filtrado para a partição do Assinante.|  
|**date_refreshed**|**datetime**|Último data em que o trabalho de instantâneo foi executado para gerar o instantâneo de dados filtrado para a partição.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifica o trabalho que cria o instantâneo de dados filtrado para uma partição.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergepartition** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** e a função de banco de dados fixa **db_owner** podem executar **sp_helpmergepartition**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergepartition](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
