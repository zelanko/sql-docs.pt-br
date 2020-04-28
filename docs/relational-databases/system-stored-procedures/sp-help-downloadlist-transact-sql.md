---
title: sp_help_downloadlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40345ed8ad1a10da0088c5c1388c44fa24cad929
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055195"
---
# <a name="sp_help_downloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista todas as linhas na tabela do sistema **sysdownloadlist** para o trabalho fornecido, ou todas as linhas, se nenhum trabalho for especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho para o qual retornar informações. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @operation = ] 'operation'`A operação válida para o trabalho especificado. a *operação* é **varchar (64)**, com um padrão de NULL e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**REMOVER**|Operação de servidor que solicita ao servidor de destino o defeito do serviço mestre **SQLSERVERAGENT** .|  
|**Delete (excluir)**|Operação de trabalho que remove um trabalho inteiro.|  
|**INSERT**|Operação de trabalho que insere um trabalho inteiro ou atualiza um trabalho existente. Esta operação inclui todas as etapas de trabalho e agendas, se aplicável.|  
|**RE-ENLIST**|Operação de servidor que faz com que o servidor de destino reenvie suas informações de inscrição, incluindo o intervalo de sondagem e o fuso horário do domínio multisservidor. O servidor de destino também baixa os detalhes do **MSXOperator** .|  
|**SET-POLL**|Operação de servidor que define o intervalo, em segundos, para que os servidores de destino sondem o domínio multisservidor. Se especificado, o *valor* será interpretado como o valor de intervalo necessário e poderá ser um valor de **10** a **28.800**.|  
|**Comece**|Operação de trabalho que solicita o início da execução do trabalho.|  
|**DEIXAR**|Operação de trabalho que solicita a parada da execução do trabalho.|  
|**SYNC-TIME**|Operação de servidor que faz com que o servidor de destino sincronize seu relógio de sistema com o domínio multisservidor. Como esta é uma operação cara, execute-a de maneira limitada e infrequente.|  
|**UPDATE**|Operação de trabalho que atualiza apenas as informações de **sysjobs** de um trabalho, não as etapas ou agendas de trabalho. É chamado automaticamente pelo **sp_update_job**.|  
  
`[ @object_type = ] 'object_type'`O tipo de objeto para o trabalho especificado. *object_type* é **varchar (64)**, com um padrão de NULL. *object_type* pode ser um trabalho ou servidor. Para obter mais informações sobre valores de *object_type*válidos, consulte [sp_add_category &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md).  
  
`[ @object_name = ] 'object_name'`O nome do objeto. *object_name* é **sysname**, com um padrão de NULL. Se *object_type* for trabalho, *object_name*será o nome do trabalho. Se *object_type*for SERVER, *object_name*será o nome do servidor.  
  
`[ @target_server = ] 'target_server'`O nome do servidor de destino. *target_server* é **nvarchar (128)**, com um padrão de NULL.  
  
`[ @has_error = ] has_error`É se o trabalho deve confirmar erros. *has_error* é **tinyint**, com um padrão de NULL, que indica que nenhum erro deve ser confirmado. **1** indica que todos os erros devem ser confirmados.  
  
`[ @status = ] status`O status do trabalho. o *status* é **tinyint**, com um valor padrão de NULL.  
  
`[ @date_posted = ] date_posted`A data e a hora em que todas as entradas feitas em ou após a data e hora especificadas devem ser incluídas no conjunto de resultados. *date_posted* é **DateTime**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Número de identificação inteiro exclusivo da instrução.|  
|**source_server**|**nvarchar(30)**|Nome do computador do servidor do qual a instrução veio. Na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7,0, esse é sempre o nome do computador do servidor mestre (MSX).|  
|**operation_code**|**nvarchar(4000)**|Código de operação da instrução.|  
|**object_name**|**sysname**|Objeto afetado pela instrução.|  
|**object_id**|**uniqueidentifier**|Número de identificação do objeto afetado pela instrução (**job_id** para um objeto de trabalho ou 0x00 para um objeto de servidor) ou um valor de dados específico para o **operation_code**.|  
|**target_server**|**nvarchar(30)**|Servidor de destino pelo qual esta instrução deve ser baixada.|  
|**error_message**|**nvarchar(1024)**|Mensagem de erro (se houver) do servidor de destino se ele encontrou um problema ao processar esta instrução.<br /><br /> Observação: qualquer mensagem de erro bloqueará todos os downloads adicionais pelo servidor de destino.|  
|**date_posted**|**datetime**|Data em que a instrução foi postada na tabela.|  
|**date_downloaded**|**datetime**|Data em que a instrução foi baixada pelo servidor de destino.|  
|**status**|**tinyint**|Status do trabalho:<br /><br /> **0** = ainda não baixado<br /><br /> **1** = baixado com êxito.|  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista as linhas no `sysdownloadlist` para o trabalho `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
