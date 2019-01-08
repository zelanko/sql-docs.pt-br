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
manager: craigg
ms.openlocfilehash: ab783933dd060c23019db5a7c16e9734e59bb140
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802278"
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@login=**] **'***logon***'**  
 É o logon do administrador do sistema a ser usado ao criar novos objetos do sistema no banco de dados de Distribuição. *login* é **sysname**, com um padrão de NULL. Esse parâmetro não é necessário se *security_mode* é definido como **1**, que é a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você está atualizando para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
 [  **@password=**] **'***senha***'**  
 É a senha do administrador do sistema a ser usada ao criar novos objetos do sistema no banco de dados de Distribuição. *senha* está **sysname**, com um padrão de **'** (cadeia de caracteres vazia). Esse parâmetro não é necessário se *security_mode* é definido como **1**, que é a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você estiver atualizando para o SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
 [  **@ver_old=**] **'***old_version***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 Esse procedimento armazenado foi preterido e será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@force_remove=**] **'***force_removal***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **'***security_mode***'**  
 É o modo de segurança do logon a ser usado ao criar novos objetos do sistema no banco de dados de Distribuição. *security_mode* está **bit** com um valor padrão de **0**. Se **0**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação será usada. Se **1**, autenticação do Windows será usada.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você está atualizando para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_vupgrade_replication** é usado ao atualizar todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_vupgrade_replication**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  
