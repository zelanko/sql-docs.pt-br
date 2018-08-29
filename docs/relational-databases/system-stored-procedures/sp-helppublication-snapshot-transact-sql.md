---
title: sp_helppublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 628b07fee13a2d0dc62d3dc5be3dfa131f995a8d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021219"
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre o Agente de Instantâneo para uma determinada publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@publisher =** ] **'***publisher***'**  
 Especifica um publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado ao adicionar um artigo a uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do Agente de Instantâneo.|  
|**name**|**nvarchar(100)**|Nome do Agente de Instantâneo.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente ao se conectar ao Publicador que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows.|  
|**publisher_login**|**sysname**|Logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar(524)**|Por motivos de segurança, um valor de **\* \* \* \* \* \* \* \* \* \*** é sempre retornado.|  
|**job_id**|**uniqueidentifier**|ID exclusiva do trabalho de agente.|  
|**job_login**|**nvarchar(512)**|É a conta de Windows na qual o Snapshot agent é executado, que é retornada no formato *domínio*\\*username*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor de **\* \* \* \* \* \* \* \* \* \*** é sempre retornado.|  
|**schedule_name**|**sysname**|Nome da agenda usado para esse trabalho do agente.|  
|**frequency_type**|**int**|É a frequência de agendamento para execução do agente, que pode ser um dos valores a seguir.<br /><br /> **1** = uma vez<br /><br /> **2** = sob demanda<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = relativo ao mês<br /><br /> **64** = iniciar automaticamente<br /><br /> **128** = recorrente|  
|**frequency_interval**|**int**|Os dias de execução do agente, que pode ter um destes valores.<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dias da semana<br /><br /> **10** = dias da semana|  
|**frequency_subday_type**|**int**|É o tipo que define a frequência com que o agente é executado quando *frequency_type* é **4** (diariamente), e pode ser um destes valores.<br /><br /> **1** = na hora especificada<br /><br /> **2** = segundos<br /><br /> **4** = minutos<br /><br /> **8** = horas|  
|**frequency_subday_interval**|**int**|Número de intervalos de *frequency_subday_type* que ocorre entre execuções programadas do agente.|  
|**frequency_relative_interval**|**int**|É a que o agente é executado em um determinado mês quando *frequency_type* é **32** (mensal relativo), e pode ser um destes valores.<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = último|  
|**frequency_recurrence_factor**|**int**|Número de semanas ou meses entre execuções programadas do agente.|  
|**active_start_date**|**int**|Data do primeiro agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_end_date**|**int**|Data do último agendamento de execução do agente, formatada como YYYYMMDD.|  
|**active_start_time**|**int**|Hora do primeiro agendamento de execução do agente, formatada como HHMMSS.|  
|**active_end_time**|**int**|Hora do último agendamento de execução do agente, formatada como HHMMSS.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_help_publication_snapshot** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa no publicador ou membros da **db_owner** banco de dados fixa do banco de dados de publicação podem executar **sp_help_publication_snapshot** .  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
