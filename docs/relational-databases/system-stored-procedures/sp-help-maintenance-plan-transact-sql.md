---
description: sp_help_maintenance_plan (Transact-SQL)
title: sp_help_maintenance_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 99fe08406840229ded741160f855ed60f11e977a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89527540"
---
# <a name="sp_help_maintenance_plan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre o plano de manutenção especificado. Se um plano não for especificado, este procedimento armazenado retornará informações sobre todos os planos de manutenção.  
  
> **Observação:** Esse procedimento armazenado é usado com planos de manutenção de banco de dados. Este recurso foi substituído por planos de manutenção que não usam esse procedimento armazenado. Use esse procedimento para manter planos de manutenção de banco de dados em instalações que foram atualizadas de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @plan_id = ] 'plan\_id'` Especifica a ID do plano do plano de manutenção. *plan_id* é **uniqueidentifier**. O padrão é NULO.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *plan_id* for especificado, **sp_help_maintenance_plan** retornará três tabelas: plano, banco de dados e trabalho.  
  
### <a name="plan-table"></a>Tabela de plano  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Identificação do plano de manutenção.|  
|**plan_name**|**sysname**|Nome do plano de manutenção.|  
|**date_created**|**datetime**|Data em que o plano de manutenção foi criado.|  
|**proprietário**|**sysname**|Proprietário do plano de manutenção.|  
|**max_history_rows**|**int**|Número máximo de linhas alocado para o registro do histórico do plano de manutenção na tabela de sistema.|  
|**remote_history_server**|**int**|O nome do servidor remoto para o qual o relatório de histórico poderia ser escrito.|  
|**max_remote_history_rows**|**int**|Número máximo de linhas alocadas na tabela do sistema em um servidor remoto no qual o relatório de histórico pode ser gravado.|  
|**user_defined_1**|**int**|O padrão é NULL.|  
|**user_defined_2**|**nvarchar (100)**|O padrão é NULL.|  
|**user_defined_3**|**datetime**|O padrão é NULL.|  
|**user_defined_4**|**uniqueidentifier**|O padrão é NULL.|  
  
### <a name="database-table"></a>Tabela de banco de dados  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**database_name**|Nome de todos os bancos de dados associados a esse plano de manutenção. *database_name* é **sysname**.|  
  
### <a name="job-table"></a>Tabela de trabalho  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**job_id**|ID de todos os trabalhos associados ao plano de manutenção. *job_id* é **uniqueidentifier**.|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_maintenance_plan** está no banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_help_maintenance_plan**.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo descreve informações sobre o plano de manutenção FAD6F2AB-3571-11D3-9D4A-00C04FB925FC.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Procedimentos armazenados do plano de manutenção de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
