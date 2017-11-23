---
title: sp_adjustpublisheridentityrange (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords: sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2f0214309eb060bbc02c7c05bf5243444ed5796
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spadjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ajusta o intervalo de identidade em uma publicação e realoca novos intervalos com base no valor de limite na publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação na qual são realocados novos intervalos de identidades. *publicação* é **sysname**, com um padrão NULL.  
  
 [  **@table_name=**] **'***table_name***'**  
 É o nome da tabela na qual são realocados novos intervalos de identidades. *table_name* é **sysname**, com um padrão NULL.  
  
 [  **@table_owner=**] **'***table_owner***'**  
 É o nome do proprietário da tabela no Publicador. *table_owner* é **sysname**, com um padrão NULL. Se *table_owner* não for especificado, o nome do usuário atual será usado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adjustpublisheridentityrange** é usado em todos os tipos de replicação.  
  
 Para uma publicação que tem o intervalo de identidade automático habilitado, o Distribution Agent ou o Merge Agent é responsável por ajustar automaticamente o intervalo de identidade em uma publicação baseada em seu valor de limite. No entanto, se por algum motivo o Distribution Agent ou Merge Agent não foi executado por um período de tempo, e o recurso de intervalo de identidade tiver sido expressivamente consumido até o ponto de limite, os usuários podem chamar **sp_adjustpublisheridentityrange** alocar um novo intervalo de valores para um publicador.  
  
 Ao executar **sp_adjustpublisheridentityrange**, *publicação* ou *table_name* deve ser especificado. Se ambos ou nenhum tiver sido especificado, um erro será ativado.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_adjustpublisheridentityrange**.  
  
## <a name="see-also"></a>Consulte também  
 [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
