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
ms.openlocfilehash: 56ed176d8b4b29e1ed4caafabd0893b7a33b1293
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962389"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
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
`[ @publication = ] 'publication'` é o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @schemaversion = ] schemaversion` identifica uma alteração de esquema pendente. *SchemaVersion* é **int**, com um valor padrão de **0**. Use [sp_enumeratependingschemachanges &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) para listar as alterações de esquema pendentes para a publicação.  
  
`[ @status = ] 'status'` é se uma alteração de esquema pendente será ignorada. *status* é **nvarchar (10)** com um valor padrão de **ativo**. Se o valor do *status* for **ignorado**, a alteração de esquema selecionada não será replicada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_markpendingschemachange** é usado com replicação de mesclagem.  
  
 **sp_markpendingschemachange** é um procedimento armazenado destinado à compatibilidade da replicação de mesclagem e deve ser usado somente quando outras ações corretivas, como reinicialização, falharam ao corrigir a situação ou são muito caras em termos de desempenho.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Consulte também  
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
