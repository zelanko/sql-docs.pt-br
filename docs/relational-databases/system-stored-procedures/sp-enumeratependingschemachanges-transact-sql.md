---
title: sp_enumeratependingschemachanges (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63ad21e40d524e2374434d733e1cc4357d6a9b23
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spenumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todas as alterações de esquema pendentes. Esse procedimento armazenado pode ser usado com [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md), que permite que um administrador a ignorar alterações de esquema pendentes selecionadas para que eles não são replicados. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@starting_schemaversion=** ] *starting_schemaversion*  
 É a alteração de esquema de número mais baixo a ser incluída no conjunto de resultados.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|Nome do artigo ao qual se aplica a alteração de esquema, ou **toda a publicação** para alterações de esquema que se aplicam a toda a publicação.|  
|**schemaversion**|**int**|O número da alteração de esquema pendente.|  
|**SchemaType**|**sysname**|Um valor de texto que representa o tipo de alteração de esquema.|  
|**schematext**|**nvarchar(max)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] que descreve a alteração de esquema.|  
|**schemastatus**|**nvarchar (10)**|Indica se uma alteração de esquema está pendente para o artigo, que pode ser um dos valores seguintes:<br /><br /> **Active** = alteração de esquema está pendente<br /><br /> **inativo** = alteração de esquema está inativa<br /><br /> **Ignorar** = alteração de esquema não será replicada|  
|**schemaguid**|**uniqueidentifier**|Identifica a alteração de esquema.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_enumeratependingschemachanges** é usado em replicação de mesclagem.  
  
 **sp_enumeratependingschemachanges**, usado com [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md), destina-se a dar suporte a replicação de mesclagem e deve ser usado somente quando outras ações corretivas, como reinicialização, falharam em corrigir a situação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_enumeratependingschemachanges**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
