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
ms.openlocfilehash: 67377f638459a37f25fbc78b9acff395192a2f3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628259"
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
 [ **@publication=** ] **'***publication***'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
`[ @schemaversion = ] schemaversion` Identifica uma alteração de esquema pendente. *schemaversion* está **int**, com um valor padrão de **0**. Use [sp_enumeratependingschemachanges &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) para listar as alterações de esquema pendente para a publicação.  
  
`[ @status = ] 'status'` É se uma alteração de esquema pendente será ignorada. *status* está **nvarchar (10)** com um valor padrão de **active**. Se o valor de *status* é **ignorada**, em seguida, a alteração de esquema selecionado não será replicada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_markpendingschemachange** é usado com replicação de mesclagem.  
  
 **sp_markpendingschemachange** é um procedimento armazenado destinado a dar suporte de replicação de mesclagem e deve ser usado somente quando outras ações corretivas, como renicialização, falharam em corrigir a situação ou são muito caras em termos de desempenho.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Consulte também  
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
