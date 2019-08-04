---
title: sp_vupgrade_replication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f6b2c736087b2f860bf8419264904e8669ba8951
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771555"
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Ativado pela instalação ao atualizar um servidor de replicação. Atualiza esquema e dados de sistema conforme o necessário para dar suporte à replicação no nível do produto atual. Cria novos objetos de sistema de replicação em bancos de dados de sistema e de usuários. Esse procedimento armazenado é executado na máquina onde a atualização da replicação deve ocorrer.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @login = ] 'login'`É o logon de administrador do sistema a ser usado ao criar novos objetos do sistema no banco de dados de distribuição. *login* é **sysname**, com um padrão de NULL. Esse parâmetro não será necessário se *security_mode* for definido como **1**, que é a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você está atualizando para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
`[ @password = ] 'password'`É a senha de administrador do sistema a ser usada ao criar novos objetos do sistema no banco de dados de distribuição. a *senha* é **sysname**, com um padrão de **' '** (cadeia de caracteres vazia). Esse parâmetro não será necessário se *security_mode* for definido como **1**, que é a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você está atualizando para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o SQL e versões posteriores.  
  
`[ @ver_old = ] 'old_version'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 Esse procedimento armazenado foi preterido e será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
`[ @force_remove = ] 'force_removal'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @security_mode = ] 'security_mode'`É o modo de segurança de logon a ser usado ao criar novos objetos do sistema no banco de dados de distribuição. *security_mode* é **bit** com um valor padrão de **0**. Sefor 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a autenticação será usada. Se **1**, a autenticação do Windows será usada.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você está atualizando para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_vupgrade_replication** é usado ao atualizar todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_vupgrade_replication**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Validar os dados replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
