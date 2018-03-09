---
title: sp_addmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e201cc5392379b09b38cf25df2e98ee2dfe96e7d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spaddmergepartition-transact-sql"></a>sp_addmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma partição dinamicamente filtrada para uma assinatura que é filtrada pelos valores de [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) ou [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) no assinante. Esse procedimento armazenado é executado no Publicador, no banco de dados que está sendo publicado, e é usado para gerar partições manualmente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication** =] **'***publicação***'**  
 É a publicação de mesclagem na qual a partição está sendo criada. *publicação* é **sysname**, sem padrão. Se *suser_sname* for especificado, o valor de *hostname* deve ser NULL.  
  
 [  **@suser_sname** =] **'***suser_sname***'**  
 É o valor usado ao criar a partição para uma assinatura filtrada pelo valor da [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) função no assinante. *suser_sname* é **sysname**, sem padrão.  
  
 [  **@host_name** =] **'***host_name***'**  
 É o valor usado ao criar a partição para uma assinatura filtrada pelo valor da [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) função no assinante. *HOST_NAME* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepartition** é usado em replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addmergepartition**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
