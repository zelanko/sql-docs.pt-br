---
title: sp_publication_validation (Transact-SQL) | Microsoft Docs
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
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c08dc184475526abd962ab97f52ccfbb8c405e8f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sppublicationvalidation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia uma solicitação de validação de artigo para cada artigo na publicação especificada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publication=**] **'***publicação '*  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [**@rowcount_only=**] *rowcount_only*  
 Especifica se apenas a contagem de linhas da tabela deve ser retornada. *rowcount_only* é **smallint** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Execute uma soma de verificação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 compatível.<br /><br /> Observação: Quando um artigo é filtrado horizontalmente, uma operação de contagem de linhas é executada em vez de uma operação de soma de verificação.|  
|**1** (padrão)|Só execute uma verificação de número de linhas.|  
|**2**|Execute uma verificação de número de linhas e soma de verificação binária.<br /><br /> Observação: Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0 assinantes, somente uma validação de número de linhas é executada.|  
  
 [**@full_or_fast=**] *full_or_fast*  
 É o método usado para calcular a contagem de linhas. *full_or_fast* é **tinyint** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Efetua contagem completa usando COUNT (*).|  
|**1**|Efetua contagem rápida de **sysindexes**. Contagem de linhas em [sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) é muito mais rápido do que contar linhas na tabela atual. No entanto, como [sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) lentamente é atualizado, o número de linhas pode não ser preciso.|  
|**2** (padrão)|Efetua contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, um COUNT(*) completo sempre será usado.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 Especifica se o Agente de Distribuição deve ou não ser desligado imediatamente após a conclusão da validação. *shutdown_agent* é **bit**, com um padrão de **0**. Se **0**, o agente de replicação não é desligado. Se **1**, o agente de replicação desligará após o último artigo é validado.  
  
 [  **@publisher**  =] **'***publicador***'**  
 Especifica um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado quando a solicitação de validação em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_publication_validation** é usado em replicação transacional.  
  
 **sp_publication_validation** pode ser chamado a qualquer momento depois que os artigos associados com a publicação tem sido ativados. O procedimento pode ser executado manualmente (uma vez) ou como parte de um trabalho agendado regularmente que valida a data.  
  
 Se seu aplicativo tiver assinantes de atualização imediata **sp_publication_validation** poderá detectar erros falsos. **sp_publication_validation** primeiro calcula o número de linhas ou a soma de verificação no publicador e, em seguida, no assinante. Como o gatilho de atualização imediata pode propagar e atualizar do Assinante para o Publicador após a conclusão do número de linhas ou da soma de verificação no Publicador, mas antes que o número de linhas ou a soma de verificação estejam concluídos no Assinante, os valores podem alterar. Para garantir que os valores no Assinante e no Publicador não sejam alterados durante a validação de uma publicação, pare o serviço MS DTC (Coordenador de Transações Distribuídas da Microsoft) no Publicador durante a validação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_publication_validation**.  
  
## <a name="see-also"></a>Consulte também  
 [Validar dados no assinante](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
