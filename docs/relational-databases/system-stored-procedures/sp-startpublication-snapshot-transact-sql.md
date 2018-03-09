---
title: sp_startpublication_snapshot (Transact-SQL) | Microsoft Docs
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
- sp_startpublication_snapshot
- sp_startpublication_snapshot_TSQL
helpviewer_keywords:
- sp_startpublication_snapshot
ms.assetid: 2cf568ee-0679-4d19-a394-27210bff61e5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fca776af212d2ffe33233c7318677893b49bc32
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spstartpublicationsnapshot-transact-sql"></a>sp_startpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado para iniciar o trabalho Agente de Instantâneo que gera o instantâneo inicial para uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_startpublication_snapshot [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@publisher=** ] **'***publicador***'**  
 É o nome de um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um valor padrão de NULL. Esse parâmetro não deve ser especificado para um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_startpublication_snapshot** é usado com todos os tipos de replicação.  
  
 Para um Editor não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_startpublication_snapshot**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)  
  
  
