---
title: sp_repladdcolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords:
- sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
author: stevestein
ms.author: sstein
ms.openlocfilehash: 75c66d1077b111837197957cc845b690b794ea24
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771046"
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Adiciona uma coluna a um artigo de tabela existente que foi publicado. Permite que a nova coluna seja adicionada a todos os Publicadores que publicam essa tabela, ou simplesmente adiciona a coluna a uma publicação específica que publica a tabela. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]
>  Esse procedimento armazenado foi preterido e tem suporte para compatibilidade com versões anteriores. Ele só deve ser usado com [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Publicadores [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e assinantes de republicação. Esse procedimento não deve ser usado em colunas com tipos de dados que foram apresentadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou superior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_repladdcolumn [ @source_object = ] 'source_object', [ @column = ] 'column' ]  
    [ , [ @typetext = ] 'typetext' ]  
    [ , [ @publication_to_add = ] 'publication_to_add' ]  
    [ , [ @from_agent = ] from_agent ]  
    [ , [ @schema_change_script = ] 'schema_change_script' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_object =] '*source_object*'  
 É o nome do artigo de tabela que contém a nova coluna a ser adicionada. *source_object* é **nvarchar (358**), sem padrão.  
  
 [ @column =] '*coluna*'  
 É o nome da coluna na tabela a ser adicionada para replicação. a *coluna* é **sysname**, sem padrão.  
  
 [ @typetext =] '*TypeText*'  
 É a definição da coluna que está sendo adicionada. *TypeText* é **nvarchar (3000)** , sem padrão. Por exemplo, se a coluna order_filled estiver sendo adicionada, e for um campo de caractere único, não NULL, e tiver um valor padrão de **N**, order_filled seria o parâmetro *Column* , enquanto a definição da coluna, **Char (1) NOT NULL restrição constraint_name DEFAULT ' n'** seria o valor do parâmetro *TypeText* .  
  
 [ @publication_to_add =] '*publication_to_add*'  
 É o nome da publicação à qual a nova coluna é adicionada. *publication_to_add* é **nvarchar (4000)** , com um padrão de **todos**. Se **tudo**, todas as publicações que contêm essa tabela serão afetadas. Se *publication_to_add* for especificado, somente essa publicação terá a nova coluna adicionada.  
  
 [ @from_agent =] *from_agent*  
 Se o procedimento armazenado estiver sendo executado por um agente de replicação. *from_agent* é **int**, com um padrão de **0**, em que um valor de **1** é usado quando esse procedimento armazenado está sendo executado por um agente de replicação e, em todos os outros casos, o valor padrão de **0**deve ser usado.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 Especifica o nome e o caminho de um script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para modificar os procedimentos armazenados personalizados gerados pelo sistema. *schema_change_script* é **nvarchar (4000)** , com um padrão de NULL. A replicação permite procedimentos armazenados personalizados definidos pelo usuário, para substituir um ou mais dos procedimentos padrão usados em replicação transacional. *schema_change_script* é executado depois que uma alteração de esquema é feita em um artigo de tabela replicada usando sp_repladdcolumn e pode ser usada para realizar uma das seguintes ações:  
  
-   Se procedimentos armazenados personalizados forem regenerados automaticamente, *schema_change_script* poderá ser usado para descartar esses procedimentos armazenados personalizados e substituí-los por procedimentos armazenados personalizados definidos pelo usuário que dão suporte ao novo esquema.  
  
-   Se procedimentos armazenados personalizados não forem regenerados automaticamente, *schema_change_script*poderá ser usado para regenerar esses procedimentos armazenados ou para criar procedimentos armazenados personalizados definidos pelo usuário.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 Habilita ou desabilita a capacidade de ter um instantâneo invalidado. *force_invalidate_snapshot* é um **bit**, com um padrão de **1**.  
  
 **1** especifica que as alterações no artigo podem fazer com que o instantâneo seja inválido e, se esse for o caso, um valor de **1** dá permissão para que o novo instantâneo ocorra.  
  
 **0** especifica que as alterações no artigo não fazem com que o instantâneo seja inválido.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 Habilita ou desabilita a capacidade de fazer com que a assinatura seja reinicializada. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que a assinatura seja reinicializada.  
  
 **1** especifica que as alterações no artigo podem fazer com que a assinatura seja reinicializada e, se esse for o caso, um valor **1** dá permissão para que a reinicialização da assinatura ocorra.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin ou da função de banco de dados fixa db_owner podem executar sp_repladdcolumn.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos preteridos no Replicação do SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
