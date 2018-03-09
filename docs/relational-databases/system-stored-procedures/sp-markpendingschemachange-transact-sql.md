---
title: sp_markpendingschemachange (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords: sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc1712e646a8efda1fdc4f06d912a1021a0beaff
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
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
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@schemaversion=** ] *schemaversion*  
 Identifica a alteração de esquema pendente. *schemaversion* é **int**, com um valor padrão de **0**. Use [sp_enumeratependingschemachanges &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) para listar as alterações de esquema pendente para a publicação.  
  
 [  **@status=** ] **'***status***'**  
 Especifica se uma alteração de esquema pendente será ignorada. *status* é **nvarchar (10)** com um valor padrão de **active**. Se o valor de *status* é **ignorada**, em seguida, a alteração de esquema selecionado não será replicada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_markpendingschemachange** é usado com a replicação de mesclagem.  
  
 **sp_markpendingschemachange** é um procedimento armazenado destinado a dar suporte a replicação de mesclagem e deve ser usado somente quando outras ações corretivas, como renicialização, falharam em corrigir a situação ou são muito caras em termos de desempenho.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Consulte também  
 [sysmergeschemachange &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
