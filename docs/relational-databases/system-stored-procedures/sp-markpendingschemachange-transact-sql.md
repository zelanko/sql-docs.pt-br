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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cea2f7c8f9ce6040f4335428e2c5e97b52a3e591
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899356"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @schemaversion = ] schemaversion`Identifica uma alteração de esquema pendente. *SchemaVersion* é **int**, com um valor padrão de **0**. Use [sp_enumeratependingschemachanges &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) para listar as alterações de esquema pendentes para a publicação.  
  
`[ @status = ] 'status'`É se uma alteração de esquema pendente será ignorada. *status* é **nvarchar (10)** com um valor padrão de **ativo**. Se o valor do *status* for **ignorado**, a alteração de esquema selecionada não será replicada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_markpendingschemachange** é usado com replicação de mesclagem.  
  
 **sp_markpendingschemachange** é um procedimento armazenado destinado à compatibilidade da replicação de mesclagem e deve ser usado somente quando outras ações corretivas, como reinicialização, falharam ao corrigir a situação ou são muito caras em termos de desempenho.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;sysmergeschemachange &#40;Transact-SQL](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
