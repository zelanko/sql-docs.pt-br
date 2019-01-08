---
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c2a269abf3e7f465c71e09437c313196e1dcd30
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205685"
---
# <a name="sprepldropcolumn-transact-sql"></a>sp_repldropcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta uma coluna de um artigo de tabela existente que foi publicado. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]
>  Esse procedimento armazenado foi preterido e só tem suporte para compatibilidade com versões anteriores. Ele só deve ser usado com [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] editores e [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes de republicação. Esse procedimento não deve ser usado em colunas com tipos de dados que foram apresentadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou superior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 É o nome do artigo de tabela que contém a nova coluna a ser removida. *source_object* é nvarchar(258), sem padrão.  
  
 [ @column =] '*coluna*'  
 É o nome da coluna na tabela a ser removida. *coluna* é sysname, sem padrão.  
  
 [ @from_agent =] *from_agent*  
 Se o procedimento armazenado estiver sendo executado por um agente de replicação. *from_agent* é int, com um padrão de 0, onde um valor de 1 é usado quando esse procedimento armazenado está sendo executado por um agente de replicação e em todos os outros casos o valor padrão de 0 deve ser usado.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 Especifica o nome e o caminho de um script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para modificar os procedimentos armazenados personalizados gerados pelo sistema. *schema_change_script* é nvarchar (4000), com um padrão NULL. A replicação permite procedimentos armazenados personalizados definidos pelo usuário, para substituir um ou mais dos procedimentos padrão usados em replicação transacional. *schema_change_script* é executado depois que uma alteração de esquema é feita em um artigo de tabela replicado usando sp_repldropcolumn e pode ser usada para fazer o seguinte:  
  
-   Se procedimentos armazenados personalizados forem gerados novamente automaticamente, *schema_change_script* pode ser usado para descartar esses procedimentos armazenados personalizados e substituí-los com definidas pelo usuário procedimentos armazenados personalizados que dá suporte ao novo esquema.  
  
-   Se procedimentos armazenados personalizados não são gerados novamente automaticamente, *schema_change_script*pode ser usado para gerar novamente esses procedimentos armazenados ou procedimentos armazenados de criar personalizado definido pelo usuário.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 Habilita ou desabilita a capacidade de ter um instantâneo invalidado. *force_invalidate_snapshot* é um pouco, com um padrão de 1.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Recursos preteridos na replicação do SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
