---
title: sp_changedistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_changedistributiondb_TSQL
- sp_changedistributiondb
helpviewer_keywords:
- sp_changedistributiondb
ms.assetid: 66f73185-ea9e-43f9-86ed-9dd933cee2f6
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4056a3cc6e8dada73358a896dbe8925b09363166
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029572"
---
# <a name="spchangedistributiondb-transact-sql"></a>sp_changedistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades do banco de dados de distribuição. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedistributiondb [ @database= ] 'database'   
    [ , [ @property= ] 'property' ]   
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database=**] **'***banco de dados***'**  
 É o nome do banco de dados de distribuição. *banco de dados* está **sysname**, sem padrão.  
  
 [  **@property=**] **'***propriedade***'**  
 É a propriedade a ser alterada para o banco de dados determinado. *propriedade* está **sysname**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**history_retention**|Período de retenção da tabela de histórico.|  
|**max_distretention**|Período máximo de retenção de distribuição.|  
|**min_distretention**|Período mínimo de retenção de distribuição.|  
|NULL (padrão)|Todos disponíveis *propriedade* valores são impressos.|  
  
 [  **@value=**] **'***valor***'**  
 É o novo valor da propriedade especificada. *valor* está **nvarchar (255)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_changedistributiondb** é usado em todos os tipos de replicação.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/sp-changedistributiondb-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_changedistributiondb**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
