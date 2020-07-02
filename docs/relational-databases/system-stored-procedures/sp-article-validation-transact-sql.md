---
title: sp_article_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a3fa3274901d881be7d52ecd62c60a802b597a0a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716257"
---
# <a name="sp_article_validation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Inicia uma solicitação de validação de dados para o artigo especificado. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação na qual o artigo existe. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo a ser validado. o *artigo* é **sysname**, sem padrão.  
  
`[ @rowcount_only = ] type_of_check_requested`Especifica se apenas o número de linhas da tabela é retornado. *type_of_check_requested* é **smallint**, com um padrão de **1**.  
  
 Se **0**, execute um número de linhas e uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] soma de verificação compatível com 7,0.  
  
 Se **1**, execute apenas uma verificação de número de linhas.  
  
 Se **2**, execute um número de linhas e uma soma de verificação binária.  
  
`[ @full_or_fast = ] full_or_fast`É o método usado para calcular o número de linhas. *full_or_fast* é **tinyint**e pode ser um desses valores.  
  
|**Valor**|**Descrição**|  
|---------------|---------------------|  
|**0**|Executa a contagem completa usando COUNT (*).|  
|**1**|Executa a contagem rápida de **sysindexes. Rows**. A contagem de linhas em **sysindexes** é mais rápida do que a contagem de linhas na tabela real. No entanto, o **sysindexes** é atualizado lentamente e o número de linhas pode não ser preciso.|  
|**2** (padrão)|Executa a contagem rápida condicional experimentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, uma contagem completa (*) sempre será usada.|  
  
`[ @shutdown_agent = ] shutdown_agent`Especifica se o Distribution Agent deve desligar imediatamente após a conclusão da validação. *shutdown_agent* é **bit**, com um padrão de **0**. Se for **0**, o agente de distribuição não será desligado. Se **1**, o agente de distribuição será desligado depois que o artigo for validado.  
  
`[ @subscription_level = ] subscription_level`Especifica se a validação é selecionada por um conjunto de assinantes. *subscription_level* é **bit**, com um padrão de **0**. Se **0**, a validação será aplicada a todos os assinantes. Se **1**, a validação será aplicada somente a um subconjunto dos assinantes especificados por chamadas para **sp_marksubscriptionvalidation** na transação aberta atual.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao solicitar a validação em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_article_validation** é usado na replicação transacional.  
  
 **sp_article_validation** faz com que informações de validação sejam coletadas no artigo especificado e posta uma solicitação de validação para o log de transações. Quando o Distribution Agent recebe essa solicitação, compara as informações de validação da solicitação com a tabela do Assinante. Os resultados de validação são exibidos no Replication Monitor e em alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente os usuários com permissões selecionar tudo na tabela de origem do artigo que está sendo validado podem executar **sp_article_validation**.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar dados replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [&#41;&#40;Transact-SQL de sp_marksubscriptionvalidation](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_publication_validation](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_table_validation](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
