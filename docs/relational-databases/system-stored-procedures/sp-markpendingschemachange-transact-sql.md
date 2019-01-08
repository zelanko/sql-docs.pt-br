---
title: sp_markpendingschemachange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba9320a155ca0af5750ca66cf10564227a3197d3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818808"
---
# <a name="spmarkpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado para dar suporte a publicações de mesclagem, habilitando um administrador a ignorar alterações de esquema pendentes selecionadas para não ser replicadas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!CAUTION]  
>  Esse procedimento armazenado pode fazer com que as alterações de esquema não sejam replicadas. Só deve ser usado para resolver problemas depois que outros métodos, como reinicialização, tenham sido tentados, ou sejam muito caros, em termos de desempenho.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@schemaversion=** ] *schemaversion*  
 Identifica a alteração de esquema pendente. *schemaversion* está **int**, com um valor padrão de **0**. Use [sp_enumeratependingschemachanges &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) para listar as alterações de esquema pendente para a publicação.  
  
 [  **@status=** ] **'***status***'**  
 Especifica se uma alteração de esquema pendente será ignorada. *status* está **nvarchar (10)** com um valor padrão de **active**. Se o valor de *status* é **ignorada**, em seguida, a alteração de esquema selecionado não será replicada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_markpendingschemachange** é usado com replicação de mesclagem.  
  
 **sp_markpendingschemachange** é um procedimento armazenado destinado a dar suporte de replicação de mesclagem e deve ser usado somente quando outras ações corretivas, como renicialização, falharam em corrigir a situação ou são muito caras em termos de desempenho.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Consulte também  
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
