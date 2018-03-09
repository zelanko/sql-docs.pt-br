---
title: sp_vupgrade_replication (Transact-SQL) | Microsoft Docs
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
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d07f50261726675d921f39226cd97f9b163b1f7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ativado pela instalação ao atualizar um servidor de replicação. Atualiza esquema e dados de sistema conforme o necessário para dar suporte à replicação no nível do produto atual. Cria novos objetos de sistema de replicação em bancos de dados de sistema e de usuários. Esse procedimento armazenado é executado na máquina onde a atualização da replicação deve ocorrer.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@login=**] **'***login***'**  
 É o logon do administrador do sistema a ser usado ao criar novos objetos do sistema no banco de dados de Distribuição. *logon* é **sysname**, com um padrão NULL. Esse parâmetro não será necessário se *security_mode* é definido como **1**, que é a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você está atualizando para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
 [  **@password=**] **'***senha***'**  
 É a senha do administrador do sistema a ser usada ao criar novos objetos do sistema no banco de dados de Distribuição. *senha* é **sysname**, com um padrão de **'** (cadeia de caracteres vazia). Esse parâmetro não será necessário se *security_mode* é definido como **1**, que é a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você estiver atualizando para o SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
 [  **@ver_old=**] **'***old_version***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 Esse procedimento armazenado foi preterido e será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@force_remove=**] **'***force_removal***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **'***security_mode***'**  
 É o modo de segurança do logon a ser usado ao criar novos objetos do sistema no banco de dados de Distribuição. *security_mode* é **bit** com um valor padrão de **0**. Se **0**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação será usada. Se **1**, a autenticação do Windows será usada.  
  
> [!NOTE]  
>  Esse parâmetro é ignorado quando você está atualizando para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_vupgrade_replication** é usada ao atualizar todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_vupgrade_replication**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  
