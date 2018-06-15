---
title: sp_restoredbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_restoredbreplication
- sp_restoredbreplication_TSQL
helpviewer_keywords:
- sp_restoredbreplication
ms.assetid: a2c5ee32-e6d9-46e9-8031-8ff13c20acf7
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ea73a77c47b4579cda2e97dcea77a8f6516157c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32996983"
---
# <a name="sprestoredbreplication-transact-sql"></a>sp_restoredbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove configurações de replicação na restauração de um banco de dados para servidor, banco de dados ou sistema que não é de origem, que de outra modo não seriam capazes de executar processos de replicação. Ao restaurar um banco de dados replicado para um servidor ou banco de dados diferente daquele de onde o backup foi feito, as configurações de replicação não podem ser preservadas. Na restauração, o servidor chama **sp_restoredbreplication** diretamente para remover automaticamente os metadados de replicação de banco de dados restaurado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_restoredbreplication [ @srv_orig = ] 'original_server_name'  
        , [ @db_orig = ] 'original_database_name'  
    [ , [ @keep_replication = ] keep_replication ]  
    [ , [ @perform_upgrade = ] perform_upgrade ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@srv_orig =** ] **'***original_server_name***'**  
 O nome do servidor onde o backup foi criado. *original_server_name* é **sysname**, sem padrão.  
  
 [  **@db_orig =** ] **'***original_database_name***'**  
 O nome do banco de dados cujo backup foi efetuado. *original_database_name* é **sysname**, sem padrão.  
  
 [  **@keep_replication =** ] *keep_replication*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@perform_upgrade=** ] *perform_upgrade*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_restoredbreplication** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** ou **dbcreator** função de servidor fixa ou **dbo** esquema de banco de dados pode executar **sp_restoredbreplication**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
