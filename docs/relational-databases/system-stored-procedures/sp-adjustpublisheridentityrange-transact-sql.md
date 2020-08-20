---
description: sp_adjustpublisheridentityrange (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9315025143c31d6fc1ef76aab4e70578e251694d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464588"
---
# <a name="sp_adjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Ajusta o intervalo de identidade em uma publicação e realoca novos intervalos com base no valor de limite na publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação na qual novos intervalos de identidade são realocados. a *publicação* é **sysname**, com um padrão de NULL.  
  
`[ @table_name = ] 'table_name'` É o nome da tabela na qual novos intervalos de identidade são realocados. *table_name* é **sysname**, com um padrão de NULL.  
  
`[ @table_owner = ] 'table_owner'` É o proprietário da tabela no Publicador. *TABLE_OWNER* é **sysname**, com um padrão de NULL. Se *TABLE_OWNER* não for especificado, o nome do usuário atual será usado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adjustpublisheridentityrange** é usado em todos os tipos de replicação.  
  
 Para uma publicação que tem o intervalo de identidade automático habilitado, o Distribution Agent ou o Merge Agent é responsável por ajustar automaticamente o intervalo de identidade em uma publicação baseada em seu valor de limite. No entanto, se por algum motivo o Agente de Distribuição ou Agente de Mesclagem não tiver sido executado por um período de tempo, e o recurso de intervalo de identidade tiver sido consumidamente muito no ponto de limite, os usuários poderão chamar **sp_adjustpublisheridentityrange** para alocar um novo intervalo de valores para um Publicador.  
  
 Ao executar **sp_adjustpublisheridentityrange**, a *publicação* ou *table_name* deve ser especificado. Se ambos ou nenhum tiver sido especificado, um erro será ativado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_adjustpublisheridentityrange**.  
  
## <a name="see-also"></a>Consulte Também  
 [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
