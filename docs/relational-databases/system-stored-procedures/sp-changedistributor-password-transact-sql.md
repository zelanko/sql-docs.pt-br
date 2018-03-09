---
title: sp_changedistributor_password (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_changedistributor_password
- sp_changedistributor_password_TSQL
helpviewer_keywords:
- sp_changedistributor_password
ms.assetid: 4a496e60-414a-4026-ba7a-3e89391d39b7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0a9eca05a9ec182d6218149d5e800fff4f5154c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangedistributorpassword-transact-sql"></a>sp_changedistributor_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera a senha para um Distribuidor. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedistributor_password [ @password= ] 'password'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@password=**] **'***senha***'**  
 É a nova senha. *senha* é **sysname**, sem padrão. Se o distribuidor for local, a senha de **distributor_admin** logon do sistema é alterado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changedistributor_password** é usado em todos os tipos de replicação.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pas_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_changedistributor_password**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)   
 [sp_adddistributor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
