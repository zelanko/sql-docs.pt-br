---
title: sp_article_validation (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed9bf6e4375c3b7afb18ffa938ae29e8d1e9e48e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia uma solicitação de validação de dados para o artigo especificado. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação na qual o artigo existe. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo a ser validado. *artigo* é **sysname**, sem padrão.  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 Especifica se apenas a contagem de linhas da tabela é retornada. *type_of_check_requested* é **smallint**, com um padrão de **1**.  
  
 Se **0**, executar um número de linhas e um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] soma de verificação compatível com 7.0.  
  
 Se **1**, executar uma verificação de número de linhas apenas.  
  
 Se **2**, executar uma soma de verificação do número de linhas e binário.  
  
 [  **@full_or_fast=**] *full_or_fast*  
 É o método usado para calcular a contagem de linhas. *full_or_fast* é **tinyint**, e pode ser um destes valores.  
  
|**Value**|**Description**|  
|---------------|---------------------|  
|**0**|Executa a contagem completa usando COUNT(*).|  
|**1**|Executa uma contagem rápida de **sysindexes**. Contagem de linhas em **sysindexes** é mais rápido que a contagem de linhas na tabela atual. No entanto, **sysindexes** é atualizado com lentidão, e o número de linhas pode não ser preciso.|  
|**2** (padrão)|Executa uma contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, um COUNT(*) completo sempre será usado.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 Especifica se o Distribution Agent deve ou não ser desligado imediatamente após a conclusão da validação. *shutdown_agent* é **bit**, com um padrão de **0**. Se **0**, o agente de distribuição não é desligado. Se **1**, o Distribution Agent desligará após o artigo é validado.  
  
 [  **@subscription_level=**] *subscription_level*  
 Especifica se a validação deve ou não ser escolhida por um conjunto de assinantes. *subscription_level* é **bit**, com um padrão de **0**. Se **0**, a validação é aplicada a todos os assinantes. Se **1**, a validação é aplicada apenas a um subconjunto de assinantes especificado por chamadas para **sp_marksubscriptionvalidation** na transação aberta atual.  
  
 [  **@reserved=**] *reservado*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher** =] **'***publicador***'**  
 Especifica um não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado quando a solicitação de validação em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_article_validation** é usado em replicação transacional.  
  
 **sp_article_validation** faz com que as informações de validação sejam coletadas no artigo especificado e envia uma solicitação de validação para o log de transações. Quando o Distribution Agent recebe essa solicitação, compara as informações de validação da solicitação com a tabela do Assinante. Os resultados de validação são exibidos no Replication Monitor e em alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente usuários com permissões SELECIONAM ALL na tabela de origem para o artigo que está sendo validado pode executar **sp_article_validation**.  
  
## <a name="see-also"></a>Consulte também  
 [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_marksubscriptionvalidation &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
