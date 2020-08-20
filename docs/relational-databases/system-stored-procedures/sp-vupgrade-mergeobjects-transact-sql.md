---
description: sp_vupgrade_mergeobjects (Transact-SQL)
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
ms.openlocfilehash: da875b534164230609015492e88b10986808c5de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480888"
---
# <a name="sp_vupgrade_mergeobjects-transact-sql"></a>sp_vupgrade_mergeobjects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @login = ] 'login'` É o logon de administrador do sistema a ser usado ao criar novos objetos do sistema no banco de dados de distribuição. *login* é **sysname**, com um padrão de NULL. Esse parâmetro não será necessário se *security_mode* for definido como **1**, que é a autenticação do Windows.  
  
`[ @password = ] 'password'` É a senha de administrador do sistema a ser usada ao criar novos objetos do sistema no banco de dados de distribuição. a *senha* é **sysname**, com um padrão de **' '** (cadeia de caracteres vazia). Esse parâmetro não será necessário se *security_mode* for definido como **1**, que é a autenticação do Windows.  
  
`[ @security_mode = ] 'security_mode'` É o modo de segurança de logon a ser usado ao criar novos objetos do sistema no banco de dados de distribuição. *security_mode* é **bit** com um valor padrão de **1**. Se for **0**, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação será usada. Se **1**, a autenticação do Windows será usada. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_vupgrade_mergeobjects** é usado somente para replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Atualizar bancos de dados replicados](../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
