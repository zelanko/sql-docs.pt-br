---
title: sp_vupgrade_mergeobjects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_mergeobjects
- sp_vupgrade_mergeobjects_TSQL
helpviewer_keywords:
- sp_vupgrade_mergeobjects
ms.assetid: 73257c2e-cc4c-48e7-9d66-7ef045bdd4f5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ec503a73e6600674e997e47670f84973236a59c2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82808522"
---
# <a name="sp_vupgrade_mergeobjects-transact-sql"></a>sp_vupgrade_mergeobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Regenera gatilhos específicos de artigo, procedimentos armazenados e exibições usadas para controlar e aplicar alterações de dados em replicação de mesclagem. Execute esse procedimento nas seguintes situações:  
  
-   Se um objeto exigido pela replicação for descartado acidentalmente.  
  
-   Se você aplicar uma atualização, como um hotfix, que requer modificação de um ou mais objetos de replicação. Execute o procedimento em cada nó depois de aplicar a atualização.  
  
 A execução desse procedimento armazenado não requer reinicialização da assinatura. Esse procedimento não será necessário se você instalar um pacote de serviço ou atualizar para uma nova  versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_vupgrade_mergeobjects [ [@login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @security_mode = ] security_mode ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @login = ] 'login'`É o logon de administrador do sistema a ser usado ao criar novos objetos do sistema no banco de dados de distribuição. *login* é **sysname**, com um padrão de NULL. Esse parâmetro não será necessário se *security_mode* for definido como **1**, que é a autenticação do Windows.  
  
`[ @password = ] 'password'`É a senha de administrador do sistema a ser usada ao criar novos objetos do sistema no banco de dados de distribuição. a *senha* é **sysname**, com um padrão de **' '** (cadeia de caracteres vazia). Esse parâmetro não será necessário se *security_mode* for definido como **1**, que é a autenticação do Windows.  
  
`[ @security_mode = ] 'security_mode'`É o modo de segurança de logon a ser usado ao criar novos objetos do sistema no banco de dados de distribuição. *security_mode* é **bit** com um valor padrão de **1**. Se for **0**, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação será usada. Se **1**, a autenticação do Windows será usada. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_vupgrade_mergeobjects** é usado somente para replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Atualizar bancos de dados replicados](../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
