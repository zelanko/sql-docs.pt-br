---
title: sp_adjustpublisheridentityrange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords:
- sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 399fe5322cb8cb5c3d20a486aac3baa810439ce7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62959670"
---
# <a name="spadjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ajusta o intervalo de identidade em uma publicação e realoca novos intervalos com base no valor de limite na publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação na qual são realocados novos intervalos de identidade. *publicação* está **sysname**, com um padrão NULL.  
  
`[ @table_name = ] 'table_name'` É o nome da tabela na qual são realocados novos intervalos de identidade. *table_name* está **sysname**, com um padrão NULL.  
  
`[ @table_owner = ] 'table_owner'` É o proprietário da tabela no publicador. *table_owner* está **sysname**, com um padrão NULL. Se *table_owner* não for especificado, o nome do usuário atual será usado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adjustpublisheridentityrange** é usado em todos os tipos de replicação.  
  
 Para uma publicação que tem o intervalo de identidade automático habilitado, o Distribution Agent ou o Merge Agent é responsável por ajustar automaticamente o intervalo de identidade em uma publicação baseada em seu valor de limite. No entanto, se por algum motivo o Distribution Agent ou Merge Agent não foi executado por um período de tempo, e o recurso de intervalo de identidade tiver sido expressivamente consumido até o ponto de limite, os usuários podem chamar **sp_adjustpublisheridentityrange** para alocar um novo intervalo de valores para um publicador.  
  
 Ao executar **sp_adjustpublisheridentityrange**, ambos *publicação* ou *table_name* deve ser especificado. Se ambos ou nenhum tiver sido especificado, um erro será ativado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_adjustpublisheridentityrange**.  
  
## <a name="see-also"></a>Consulte também  
 [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
