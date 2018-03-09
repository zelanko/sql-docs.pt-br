---
title: sp_repladdcolumn (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords: sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d638619d087d43b0820fdf21650a9b8db1f7cf63
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma coluna a um artigo de tabela existente que foi publicado. Permite que a nova coluna seja adicionada a todos os Publicadores que publicam essa tabela, ou simplesmente adiciona a coluna a uma publicação específica que publica a tabela. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Esse procedimento armazenado foi preterido e tem suporte para compatibilidade com versões anteriores. Ele só deve ser usado com [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] editores e [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes de republicação. Esse procedimento não deve ser usado em colunas com tipos de dados que foram apresentadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou superior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 É o nome da coluna na tabela a ser adicionada para replicação. *coluna* é **sysname**, sem padrão.  
  
 [ @typetext =] '*typetext*'  
 É a definição da coluna que está sendo adicionada. *TypeText* é **nvarchar (3000)**, sem padrão. Por exemplo, se a coluna order_filled estiver sendo adicionada e for um único caractere campo, não NULL e tem um valor padrão de **N**, order_filled seria o *coluna* parâmetro, enquanto a definição do coluna, **char (1) não NULL CONSTRAINT constraint_name DEFAULT ' n'** seria o *typetext* o valor do parâmetro.  
  
 [ @publication_to_add =] '*publication_to_add*'  
 É o nome da publicação à qual a nova coluna é adicionada. *publication_to_add* é **nvarchar (4000)**, com um padrão de **todos os**. Se **todos os**, em seguida, todas as publicações que contém esta tabela são afetadas. Se *publication_to_add* for especificado, somente esta publicação terá a nova coluna adicionada.  
  
 [ @from_agent =] *from_agent*  
 Se o procedimento armazenado estiver sendo executado por um agente de replicação. *from_agent* é **int**, com um padrão de **0**, onde um valor de **1** é usado quando esse procedimento armazenado está sendo executado por um agente de replicação e no qualquer outro caso, o valor padrão de **0**devem ser usados.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 Especifica o nome e o caminho de um script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para modificar os procedimentos armazenados personalizados gerados pelo sistema. *schema_change_script* é **nvarchar (4000)**, com um padrão NULL. A replicação permite procedimentos armazenados personalizados definidos pelo usuário, para substituir um ou mais dos procedimentos padrão usados em replicação transacional. *schema_change_script* é executado depois que uma alteração de esquema é feita em um artigo de tabela replicado usando sp_repladdcolumn e pode ser usada para fazer o seguinte:  
  
-   Se procedimentos armazenados personalizados forem gerados novamente automaticamente, *schema_change_script* pode ser usado para descartar esses procedimentos armazenados personalizados e substituí-las por definido pelo usuário procedimentos armazenados personalizados que oferece suporte ao novo esquema.  
  
-   Se procedimentos armazenados personalizados não são geradas novamente automaticamente, *schema_change_script*pode ser usado para gerar novamente esses procedimentos armazenados ou personalizados definidos pelo usuário de criar procedimentos armazenados.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 Habilita ou desabilita a capacidade de ter um instantâneo invalidado. *force_invalidate_snapshot* é um **bit**, com um padrão de **1**.  
  
 **1** Especifica que as alterações no artigo podem invalidar o instantâneo, e se esse for o caso, um valor de **1** dá permissão para a ocorrência do novo instantâneo.  
  
 **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 Habilita ou desabilita a capacidade de fazer com que a assinatura seja reinicializada. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que a assinatura ser reiniciada.  
  
 **1** Especifica que as alterações no artigo podem invalidar a assinatura ser reiniciada, e se esse for o caso, um valor de **1** dá permissão para que ocorra a reinicialização da assinatura.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin ou da função de banco de dados fixa db_owner podem executar sp_repladdcolumn.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos preteridos no SQL Server Replication](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
