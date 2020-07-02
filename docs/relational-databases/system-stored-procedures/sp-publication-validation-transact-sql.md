---
title: sp_publication_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: db8a79e723d76cdf54377618cc94cb6a4b5431d7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715184"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Inicia uma solicitação de validação de artigo para cada artigo na publicação especificada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @rowcount_only = ] 'rowcount_only'`É se deve retornar apenas o número de linhas da tabela. *rowcount_only* é **smallint** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Execute uma soma de verificação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 compatível.<br /><br /> Observação: quando um artigo é filtrado horizontalmente, uma operação de número de linhas é executada em vez de uma operação de soma de verificação.|  
|**1** (padrão)|Só execute uma verificação de número de linhas.|  
|**2**|Execute uma verificação de número de linhas e soma de verificação binária.<br /><br /> Observação: para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes da versão 7,0, apenas uma validação de número de linhas é executada.|  
  
`[ @full_or_fast = ] 'full_or_fast'`É o método usado para calcular o número de linhas. *full_or_fast* é **tinyint** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Efetua contagem completa usando COUNT (*).|  
|**1**|A contagem rápida de **sysindexes. Rows**. A contagem de linhas em [sys.sysíndices](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) é muito mais rápida do que a contagem de linhas na tabela real. No entanto, como [sys.sysíndices](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) é atualizado lentamente, o número de linhas pode não ser preciso.|  
|**2** (padrão)|Efetua contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, uma contagem completa (*) sempre será usada.|  
  
`[ @shutdown_agent = ] 'shutdown_agent'`É se o Agente de Distribuição deve desligar imediatamente após a conclusão da validação. *shutdown_agent* é **bit**, com um padrão de **0**. Se for **0**, o agente de replicação não será desligado. Se for **1**, o agente de replicação será desligado depois que o último artigo for validado.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao solicitar a validação em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_publication_validation** é usado na replicação transacional.  
  
 **sp_publication_validation** pode ser chamado a qualquer momento depois que os artigos associados à publicação forem ativados. O procedimento pode ser executado manualmente (uma vez) ou como parte de um trabalho agendado regularmente que valida a data.  
  
 Se seu aplicativo tiver assinantes de atualização imediata, **sp_publication_validation** poderá detectar erros falsos. **sp_publication_validation** primeiro calcula o número de linhas ou soma de verificação no Publicador e, em seguida, no Assinante. Como o gatilho de atualização imediata pode propagar e atualizar do Assinante para o Publicador após a conclusão do número de linhas ou da soma de verificação no Publicador, mas antes que o número de linhas ou a soma de verificação estejam concluídos no Assinante, os valores podem alterar. Para garantir que os valores no Assinante e no Publicador não sejam alterados durante a validação de uma publicação, pare o serviço MS DTC (Coordenador de Transações Distribuídas da Microsoft) no Publicador durante a validação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_publication_validation**.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar dados no Assinante](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [&#41;&#40;Transact-SQL de sp_article_validation](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_table_validation](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
