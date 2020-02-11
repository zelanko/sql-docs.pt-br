---
title: sp_changedistributor_password (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributor_password
- sp_changedistributor_password_TSQL
helpviewer_keywords:
- sp_changedistributor_password
ms.assetid: 4a496e60-414a-4026-ba7a-3e89391d39b7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3715bfacd1a94f588992d7e6832814f50c076d1c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68768897"
---
# <a name="sp_changedistributor_password-transact-sql"></a>sp_changedistributor_password (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Altera a senha para um Distribuidor. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedistributor_password [ @password= ] 'password'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @password = ] 'password'`É a nova senha. a *senha* é **sysname**, sem padrão. Se o distribuidor for local, a senha do logon do sistema **distributor_admin** será alterada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changedistributor_password** é usado em todos os tipos de replicação.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pas_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_changedistributor_password**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Proteger o distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)   
 [&#41;&#40;Transact-SQL de sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
