---
title: sp_dropdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8060e5788004b743e58e0d0d424dcc0910459573
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spdropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta um Publicador de distribuição. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publicador***'**  
 É o Publicador a ser removido. *publicador* é **sysname**, sem padrão.  
  
 [  **@no_checks=** ] *no_checks*  
 Especifica se **sp_dropdistpublisher** verifica se o publicador desinstalou o servidor como distribuidor. *no_checks* é **bit**, com um padrão de **0**.  
  
 Se **0**, replicação verificará se o publicador remoto desinstalou o servidor local como o distribuidor. Se o Publicador for local, a replicação verificará se não há objetos de publicação ou distribuição restantes no servidor local.  
  
 Se **1**, todos os objetos de replicação associados com o publicador de distribuição são descartados, mesmo que um publicador remoto não pode ser alcançado. Depois de fazer isso, o publicador remoto deve desinstalar a replicação usando [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) com  **@ignore_distributor**   =  **1**.  
  
 [  **@ignore_distributor=** ] *ignore_distributor*  
 Especifica se os objetos de distribuição são deixados no Distribuidor quando o Publicador é removido. *ignore_distributor* é **bit** e pode ser um destes valores:  
  
 **1** = objetos de distribuição que pertencem ao *publicador* permanecem no distribuidor.  
  
 **0** = objetos de distribuição para o *publicador* são limpos no distribuidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropdistpublisher** é usado em todos os tipos de replicação.  
  
 Ao descartar um publicador Oracle, se não for possível descartar o editor **sp_dropdistpublisher** retorna um erro e os objetos do distribuidor para o publicador são removidos.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_dropdistpublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
