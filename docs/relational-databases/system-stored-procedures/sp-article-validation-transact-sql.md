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
manager: craigg
ms.openlocfilehash: 849564fcda37c022413d9e0758abe50279497a0b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54125101"
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
 [  **@publication=**] **'**_publicação_**'**  
 É o nome da publicação na qual o artigo existe. *publicação* está **sysname**, sem padrão.  
  
 [  **@article=**] **'**_artigo_**'**  
 É o nome do artigo a ser validado. *artigo* está **sysname**, sem padrão.  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 Especifica se apenas a contagem de linhas da tabela é retornada. *type_of_check_requested* está **smallint**, com um padrão de **1**.  
  
 Se **0**, execute um número de linhas e uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] soma de verificação compatível com 7.0.  
  
 Se **1**, executar apenas uma verificação de número de linhas.  
  
 Se **2**, executar uma soma de verificação do número de linhas e binário.  
  
 [  **@full_or_fast=**] *full_or_fast*  
 É o método usado para calcular a contagem de linhas. *full_or_fast* está **tinyint**, e pode ser um destes valores.  
  
|**Value**|**Descrição**|  
|---------------|---------------------|  
|**0**|Executa a contagem completa usando COUNT(*).|  
|**1**|Executa uma contagem rápida de **sysindexes**. Contagem de linhas em **sysindexes** é mais rápido do que contar linhas na tabela atual. No entanto, **sysindexes** é atualizado com lentidão, e o número de linhas pode não ser preciso.|  
|**2** (padrão)|Executa uma contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, um COUNT(*) completo sempre será usado.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 Especifica se o Distribution Agent deve ou não ser desligado imediatamente após a conclusão da validação. *shutdown_agent* está **bit**, com um padrão de **0**. Se **0**, o agente de distribuição não é desligado. Se **1**, o Distribution Agent desligará após o artigo é validado.  
  
 [  **@subscription_level=**] *subscription_level*  
 Especifica se a validação deve ou não ser escolhida por um conjunto de assinantes. *subscription_level* está **bit**, com um padrão de **0**. Se **0**, validação é aplicada a todos os assinantes. Se **1**, validação é aplicada somente a um subconjunto de assinantes especificado por chamadas para **sp_marksubscriptionvalidation** na transação aberta atual.  
  
 [  **@reserved=**] *reservado*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@publisher**=] **'**_publisher_**'**  
 Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
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
  
  
