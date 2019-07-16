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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4c9d0a82422675c9698d7216b92e1c9401392a79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004825"
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia uma solicitação de validação de dados para o artigo especificado. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` É o nome da publicação na qual o artigo existe. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo para validar. *artigo* está **sysname**, sem padrão.  
  
`[ @rowcount_only = ] type_of_check_requested` Especifica se apenas o número de linhas da tabela é retornado. *type_of_check_requested* está **smallint**, com um padrão de **1**.  
  
 Se **0**, execute um número de linhas e uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] soma de verificação compatível com 7.0.  
  
 Se **1**, executar apenas uma verificação de número de linhas.  
  
 Se **2**, executar uma soma de verificação do número de linhas e binário.  
  
`[ @full_or_fast = ] full_or_fast` O método é usado para calcular o número de linhas. *full_or_fast* está **tinyint**, e pode ser um destes valores.  
  
|**Valor**|**Descrição**|  
|---------------|---------------------|  
|**0**|Executa a contagem completa usando COUNT(*).|  
|**1**|Executa uma contagem rápida de **sysindexes**. Contagem de linhas em **sysindexes** é mais rápido do que contar linhas na tabela atual. No entanto, **sysindexes** é atualizado com lentidão, e o número de linhas pode não ser preciso.|  
|**2** (padrão)|Executa uma contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, um COUNT(*) completo sempre será usado.|  
  
`[ @shutdown_agent = ] shutdown_agent` Especifica se o Distribution agent deve desligado imediatamente após a conclusão da validação. *shutdown_agent* está **bit**, com um padrão de **0**. Se **0**, o agente de distribuição não é desligado. Se **1**, o Distribution Agent desligará após o artigo é validado.  
  
`[ @subscription_level = ] subscription_level` Especifica se a validação é captada por um conjunto de assinantes. *subscription_level* está **bit**, com um padrão de **0**. Se **0**, validação é aplicada a todos os assinantes. Se **1**, validação é aplicada somente a um subconjunto de assinantes especificado por chamadas para **sp_marksubscriptionvalidation** na transação aberta atual.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado ao solicitar uma validação em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_article_validation** é usado em replicação transacional.  
  
 **sp_article_validation** faz com que as informações de validação sejam coletadas no artigo especificado e envia uma solicitação de validação para o log de transações. Quando o Distribution Agent recebe essa solicitação, compara as informações de validação da solicitação com a tabela do Assinante. Os resultados de validação são exibidos no Replication Monitor e em alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente usuários com permissões SELECIONAM ALL na tabela de origem para o artigo que está sendo validado pode executar **sp_article_validation**.  
  
## <a name="see-also"></a>Consulte também  
 [Validar os dados replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
