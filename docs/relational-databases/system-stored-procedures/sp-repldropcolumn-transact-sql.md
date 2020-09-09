---
description: sp_repldropcolumn (Transact-SQL)
title: sp_repldropcolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldropcolumn_TSQL
- sp_repldropcolumn
helpviewer_keywords:
- sp_repldropcolumn
ms.assetid: fdc1ec5f-f108-42b4-a2d8-f06a71913ab8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: df9b2be3d6253bd3ba225d4cc444e705678109f3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534928"
---
# <a name="sp_repldropcolumn-transact-sql"></a>sp_repldropcolumn (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Descarta uma coluna de um artigo de tabela existente que foi publicado. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]
>  Esse procedimento armazenado foi preterido e só tem suporte para compatibilidade com versões anteriores. Ele só deve ser usado com [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Publicadores e [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes de republicação. Esse procedimento não deve ser usado em colunas com tipos de dados que foram apresentadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou superior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_repldropcolumn [ @source_object = ] 'source_object', [ @column = ] 'column'   
    [ , [ @from_agent = ] from_agent]   
    [ , [ @schema_change_script = ] 'schema_change_script' ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_object =] '*source_object*'  
 É o nome do artigo de tabela que contém a nova coluna a ser removida. *source_object* é nvarchar (258), sem padrão.  
  
 [ @column =] '*coluna*'  
 É o nome da coluna na tabela a ser removida. a *coluna* é sysname, sem padrão.  
  
 [ @from_agent =] *from_agent*  
 Se o procedimento armazenado estiver sendo executado por um agente de replicação. *from_agent* é int, com um padrão de 0, em que um valor de 1 é usado quando esse procedimento armazenado está sendo executado por um agente de replicação e, em todos os casos, o valor padrão de 0 deve ser usado.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 Especifica o nome e o caminho de um script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para modificar os procedimentos armazenados personalizados gerados pelo sistema. *schema_change_script* é nvarchar (4000), com um padrão de NULL. A replicação permite procedimentos armazenados personalizados definidos pelo usuário, para substituir um ou mais dos procedimentos padrão usados em replicação transacional. *schema_change_script* é executado depois que uma alteração de esquema é feita em um artigo de tabela replicada usando sp_repldropcolumn e pode ser usada para realizar uma das seguintes ações:  
  
-   Se procedimentos armazenados personalizados forem regenerados automaticamente, *schema_change_script* poderá ser usado para descartar esses procedimentos armazenados personalizados e substituí-los por procedimentos armazenados personalizados definidos pelo usuário que dão suporte ao novo esquema.  
  
-   Se procedimentos armazenados personalizados não forem regenerados automaticamente, *schema_change_script*poderá ser usado para regenerar esses procedimentos armazenados ou para criar procedimentos armazenados personalizados definidos pelo usuário.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 Habilita ou desabilita a capacidade de ter um instantâneo invalidado. *force_invalidate_snapshot* é um bit, com um padrão de 1.  
  
 1 especifica que as alterações no artigo podem invalidar o instantâneo e, se esse for o caso, um valor de 1 dá permissão para a ocorrência do novo instantâneo.  
  
 0 especifica que as alterações no artigo não invalidam o instantâneo.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 Habilita ou desabilita a capacidade de fazer com que a assinatura seja reinicializada. *force_reinit_subscription* é um bit com um padrão de 0.  
  
 0 especifica que as alterações no artigo não fazem com que a assinatura seja reiniciada.  
  
 1 especifica que alterações no artigo podem fazer com que a assinatura seja reiniciada e, se esse for o caso, um valor de 1 dará permissão para que a assinatura seja reiniciada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin no Publicador, ou membros das funções de banco de dados fixa db_owner ou db_ddladmin no banco de dados de publicação, podem executar sp_repldropcolumn.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos preteridos no Replicação do SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
