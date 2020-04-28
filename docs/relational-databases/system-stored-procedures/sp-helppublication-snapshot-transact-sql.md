---
title: sp_helppublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
author: stevestein
ms.author: sstein
ms.openlocfilehash: d8909396e7a7da39ed2ae27c475a154c58bad090
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771499"
---
# <a name="sp_helppublication_snapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações sobre o Agente de Instantâneo para uma determinada publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao adicionar um artigo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um Publicador.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do Agente de Instantâneo.|  
|**name**|**nvarchar (100)**|Nome do Agente de Instantâneo.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente ao se conectar ao Publicador que pode ser um dos seguintes:<br /><br /> **0** =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows.|  
|**publisher_login**|**sysname**|Logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar (524)**|Por motivos de segurança, um valor ** \* \* \* \* \* \* \* \* de \* ** é sempre retornado.|  
|**job_id**|**uniqueidentifier**|ID exclusiva do trabalho de agente.|  
|**job_login**|**nvarchar(512)**|É a conta do Windows na qual o Snapshot Agent é executado, que é retornado no formato *domínio*\\*nome de usuário*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor ** \* \* \* \* \* \* \* \* de \* ** é sempre retornado.|  
|**schedule_name**|**sysname**|Nome da agenda usado para esse trabalho do agente.|  
|**frequency_type**|**int**|É a frequência de agendamento para execução do agente, que pode ser um dos valores a seguir.<br /><br /> **1** = uma vez<br /><br /> **2** = sob demanda<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = relativo mensal<br /><br /> **64** = inicialização automática<br /><br /> **128** = recorrente|  
|**frequency_interval**|**int**|Os dias de execução do agente, que pode ter um destes valores.<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dias da semana<br /><br /> **10** = dias de semana|  
|**frequency_subday_type**|**int**|É o tipo que define a frequência com que o agente é executado quando *frequency_type* é **4** (diariamente) e pode ser um desses valores.<br /><br /> **1** = na hora especificada<br /><br /> **2** = segundos<br /><br /> **4** = minutos<br /><br /> **8** = horas|  
|**frequency_subday_interval**|**int**|Número de intervalos de *frequency_subday_type* que ocorrem entre a execução agendada do agente.|  
|**frequency_relative_interval**|**int**|É a semana em que o agente é executado em um determinado mês quando *frequency_type* é **32** (relativo mensal) e pode ser um desses valores.<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = última|  
|**frequency_recurrence_factor**|**int**|Número de semanas ou meses entre execuções programadas do agente.|  
|**active_start_date**|**int**|Data do primeiro agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_end_date**|**int**|Data do último agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_start_time**|**int**|Hora do primeiro agendamento de execução do agente, formatada como HHMMSS.|  
|**active_end_time**|**int**|Hora do último agendamento de execução do agente, formatada como HHMMSS.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_help_publication_snapshot** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no Publicador ou membros da função de banco de dados fixa **db_owner** no banco de dados de publicação podem ser executados **sp_help_publication_snapshot**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication_snapshot](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergepublication](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droppublication](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
