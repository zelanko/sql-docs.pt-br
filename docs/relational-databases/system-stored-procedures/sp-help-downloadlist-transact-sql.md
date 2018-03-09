---
title: sp_help_downloadlist (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c768ab8d8908d6c62805539e3fb811cee293da55
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpdownloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista todas as linhas de **sysdownloadlist** tabela do sistema para o trabalho fornecido, ou todas as linhas se nenhum trabalho for especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@job_id=** ] *job_id*  
 O número de identificação do trabalho para o qual as informações devem ser retornadas. *job_id* é **uniqueidentifier**, com um padrão NULL.  
  
 [ **@job_name=** ] **'***job_name***'**  
 O nome do trabalho. *job_name* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  O *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [  **@operation=** ] **'***operação***'**  
 A operação válida para o trabalho especificado. *operação* é **varchar(64)**, com um padrão NULL, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**DEFECT**|Operação de servidor que solicita o servidor de destino para remover do mestre **SQLServerAgent** serviço.|  
|**DELETE**|Operação de trabalho que remove um trabalho inteiro.|  
|**INSERT**|Operação de trabalho que insere um trabalho inteiro ou atualiza um trabalho existente. Esta operação inclui todas as etapas de trabalho e agendas, se aplicável.|  
|**RE-ENLIST**|Operação de servidor que faz com que o servidor de destino reenvie suas informações de inscrição, incluindo o intervalo de sondagem e o fuso horário do domínio multisservidor. O servidor de destino também baixa novamente o **MSXOperator** detalhes.|  
|**SET-POLL**|Operação de servidor que define o intervalo, em segundos, para que os servidores de destino sondem o domínio multisservidor. Se especificado, *valor* é interpretado como o valor de intervalo necessário, e pode ser um valor de **10** para **28.800**.|  
|**START**|Operação de trabalho que solicita o início da execução do trabalho.|  
|**STOP**|Operação de trabalho que solicita a parada da execução do trabalho.|  
|**SYNC-TIME**|Operação de servidor que faz com que o servidor de destino sincronize seu relógio de sistema com o domínio multisservidor. Como esta é uma operação cara, execute-a de maneira limitada e infrequente.|  
|**UPDATE**|Operação de trabalho que atualiza apenas o **sysjobs** informações para um trabalho, não as etapas de trabalho ou agendas. É chamado automaticamente pelo **sp_update_job**.|  
  
 [ **@object_type=** ] **'***object_type***'**  
 O tipo do objeto para o trabalho especificado. *object_type* é **varchar(64)**, com um padrão NULL. *object_type* pode ser JOB ou SERVER. Para obter mais informações sobre válido *object_type*valores, consulte [sp_add_category &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md).  
  
 [ **@object_name=** ] **'***object_name***'**  
 O nome do objeto. *object_name* é **sysname**, com um padrão NULL. Se *object_type* for JOB, *object_name*é o nome do trabalho. Se *object_type*é o servidor, *object_name*é o nome do servidor.  
  
 [ **@target_server=** ] **'***target_server***'**  
 O nome do servidor de destino. *target_server* é **nvarchar (128)**, com um padrão NULL.  
  
 [ **@has_error=** ] *has_error*  
 Especifica se o trabalho deve confirmar erros. *has_error* é **tinyint**, com um padrão NULL, que indica que nenhum erro deve ser confirmado. **1** indica que todos os erros devem ser confirmados.  
  
 [ **@status=** ] *status*  
 O status do trabalho. *status* é **tinyint**, com um valor padrão de NULL.  
  
 [ **@date_posted=** ] *date_posted*  
 A data e a hora a partir das quais todas as entradas feitas na data e hora especificadas ou depois devem ser incluídas no conjunto de resultados. *date_posted* é **datetime**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**Int**|Número de identificação inteiro exclusivo da instrução.|  
|**source_server**|**nvarchar(30)**|Nome do computador do servidor do qual a instrução veio. Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0, sempre é o nome do computador do servidor mestre (MSX).|  
|**operation_code**|**nvarchar(4000)**|Código de operação da instrução.|  
|**object_name**|**sysname**|Objeto afetado pela instrução.|  
|**object_id**|**uniqueidentifier**|Número de identificação do objeto afetado pela instrução (**job_id** para um objeto de trabalho ou 0x00 para um objeto de servidor) ou um valor de dados específico a **operation_code**.|  
|**target_server**|**nvarchar(30)**|Servidor de destino pelo qual esta instrução deve ser baixada.|  
|**error_message**|**nvarchar(1024)**|Mensagem de erro (se houver) do servidor de destino se ele encontrou um problema ao processar esta instrução.<br /><br /> Observação: Qualquer mensagem de erro bloqueia todos os downloads adicionais pelo servidor de destino.|  
|**date_posted**|**datetime**|Data em que a instrução foi postada na tabela.|  
|**date_downloaded**|**datetime**|Data em que a instrução foi baixada pelo servidor de destino.|  
|**status**|**tinyint**|Status do trabalho:<br /><br /> **0** = ainda não baixado<br /><br /> **1** = baixado com êxito.|  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar esse procedimento usam como padrão membros da função de servidor fixa **sysadmin** .  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
