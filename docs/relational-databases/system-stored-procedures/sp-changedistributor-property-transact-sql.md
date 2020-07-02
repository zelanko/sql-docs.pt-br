---
title: sp_changedistributor_property (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributor_property_TSQL
- sp_changedistributor_property
helpviewer_keywords:
- sp_changedistributor_property
ms.assetid: 04f503a1-307c-4de0-bac6-e6e97d5b6940
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 441fe87551fd06ba786b4b36589bea00d7d399b9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771533"
---
# <a name="sp_changedistributor_property-transact-sql"></a>sp_changedistributor_property (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera as propriedades do Distribuidor. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedistributor_property [ [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @property = ] 'property'`É a propriedade para um determinado distribuidor. a *Propriedade* é **sysname**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**heartbeat_interval**|Número máximo de minutos que um agente pode executar sem registrar uma mensagem de progresso.|  
|NULL (padrão)|Todos os valores de *Propriedade* disponíveis são impressos.|  
  
`[ @value = ] 'value'`É o valor para a propriedade de distribuidor fornecida. o *valor* é **varchar (255)**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changedistributor_property** é usado em todos os tipos de replicação.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pro_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_changedistributor_property**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as propriedades do distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [&#41;&#40;Transact-SQL de sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
