---
title: sp_enumeratependingschemachanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
author: stevestein
ms.author: sstein
ms.openlocfilehash: da5579c52d1ffe1400e3b4c8c01210ca5856597b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124576"
---
# <a name="sp_enumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todas as alterações de esquema pendentes. Esse procedimento armazenado pode ser usado com [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md), o que permite que um administrador ignore as alterações de esquema pendentes selecionadas para que elas não sejam replicadas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @starting_schemaversion = ] starting_schemaversion`É a alteração de esquema de número mais baixo a ser incluída no conjunto de resultados.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|Nome do artigo ao qual se aplica a alteração de esquema ou a **toda a publicação** para alterações de esquema que se aplicam à publicação inteira.|  
|**SchemaVersion**|**int**|O número da alteração de esquema pendente.|  
|**schematype**|**sysname**|Um valor de texto que representa o tipo de alteração de esquema.|  
|**schematext**|**nvarchar(max)**|
  [!INCLUDE[tsql](../../includes/tsql-md.md)] que descreve a alteração de esquema.|  
|**schemastatus**|**nvarchar (10)**|Indica se uma alteração de esquema está pendente para o artigo, que pode ser um dos valores seguintes:<br /><br /> **ativo** = alteração de esquema pendente<br /><br /> **inativo** = alteração de esquema está inativa<br /><br /> **ignorar** = alteração de esquema não é replicada|  
|**schemaguid**|**uniqueidentifier**|Identifica a alteração de esquema.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_enumeratependingschemachanges** é usado na replicação de mesclagem.  
  
 **sp_enumeratependingschemachanges**, usado com [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md), destina-se à compatibilidade da replicação de mesclagem e deve ser usado somente quando outras ações corretivas, como reinicialização, falharam ao corrigir a situação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_enumeratependingschemachanges**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [&#41;sysmergeschemachange &#40;Transact-SQL](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
