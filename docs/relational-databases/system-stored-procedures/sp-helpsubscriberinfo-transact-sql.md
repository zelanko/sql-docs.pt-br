---
title: sp_helpsubscriberinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriberinfo
- sp_helpsubscriberinfo_TSQL
helpviewer_keywords:
- sp_helpsubscriberinfo
ms.assetid: fbabe1ec-57cf-425c-bae7-af7f5d3198fd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38b653dcb51f428692401fb87609187a82449393
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771493"
---
# <a name="sp_helpsubscriberinfo-transact-sql"></a>sp_helpsubscriberinfo (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Exibe informações sobre um Assinante. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsubscriberinfo [ [ @subscriber =] 'subscriber']  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o assinante é **sysname**, com um **%** padrão de, que retorna todas as informações.  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o Publicador é **sysname**e usa como padrão o nome do servidor atual.  
  
> [!NOTE]  
>  o Publicador não deve ser especificado, exceto quando é um Publicador Oracle.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome do Publicador.|  
|**Assinante**|**sysname**|Nome do Assinante.|  
|**type**|**tinyint**|O tipo de Assinante:<br /><br /> **0**  = Database1 = fonte de dados ODBC [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**login**|**sysname**|ID de logon para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**sysname**|Senha para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**commit_batch_size**|**int**|Sem suporte.|  
|**status_batch_size**|**int**|Sem suporte.|  
|**flush_frequency**|**int**|Sem suporte.|  
|**frequency_type**|**int**|Frequência com que o Distribution Agent é executado:<br /><br /> **1** = uma vez<br /><br /> **2** = sob demanda<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = relativo mensal<br /><br /> **64** = inicialização automática<br /><br /> **128** = recorrente|  
|**frequency_interval**|**int**|Valor aplicado à frequência definida por *frequency_type*.|  
|**frequency_relative_interval**|**int**|Data do Agente de Distribuição usado quando *frequency_type* é definido como **32** (relativo mensal):<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = última|  
|**frequency_recurrence_factor**|**int**|Fator de recorrência usado pelo *frequency_type*.|  
|**frequency_subday**|**int**|Frequência de reagendamento durante o período definido:<br /><br /> **1** = uma vez<br /><br /> **2** = segundo<br /><br /> **4** = minuto<br /><br /> **8** = hora|  
|**frequency_subday_interval**|**int**|Intervalo para *frequency_subday*.|  
|**active_start_time_of_day**|**int**|Hora do dia do primeiro agendamento do Distribution Agent, formatada como HHMMSS.|  
|**active_end_time_of_day**|**int**|Hora de dia do último agendamento do Distribution Agent, formatada como HHMMSS.|  
|**active_start_date**|**int**|Data do primeiro agendamento do Distribution Agent, formatada como YYYYMMDD.|  
|**active_end_date**|**int**|Data do último agendamento do Distribution Agent, formatada como YYYYMMDD.|  
|**retryattempt**|**int**|Sem suporte.|  
|**retrydelay**|**int**|Sem suporte.|  
|**description**|**nvarchar(255)**|Descrição de texto do Assinante.|  
|**security_mode**|**int**|Modo de segurança implementado:<br /><br /> **0**  =  autenticação[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 =  autenticaçãodoWindows[!INCLUDE[msCoName](../../includes/msconame-md.md)]|  
|**frequency_type2**|**int**|Frequência de execução do Merge Agent:<br /><br /> **1** = uma vez<br /><br /> **2** = sob demanda<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = relativo mensal<br /><br /> **64** = inicialização automática<br /><br /> **128** = recorrente|  
|**frequency_interval2**|**int**|Valor aplicado à frequência definida por *frequency_type*.|  
|**frequency_relative_interval2**|**int**|Data do Agente de Mesclagem usado quando *frequency_type* é definido como 32 (relativo mensal):<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = última|  
|**frequency_recurrence_factor2**|**int**|Fator de recorrência usado por *frequency_type * *.*|  
|**frequency_subday2**|**int**|Frequência de reagendamento durante o período definido:<br /><br /> **1** = uma vez<br /><br /> **2** = segundo<br /><br /> **4** = minuto<br /><br /> **8** = hora|  
|**frequency_subday_interval2**|**int**|Intervalo para *frequency_subday*.|  
|**active_start_time_of_day2**|**int**|Hora de dia do primeiro agendamento do Merge Agent, formatada como HHMMSS.|  
|**active_end_time_of_day2**|**int**|Hora de dia do último agendamento do Merge Agent, formatada como HHMMSS.|  
|**active_start_date2**|**int**|Data do primeiro agendamento do Merge Agent, formatada como YYYYMMDD.|  
|**active_end_date2**|**int**|Data do último agendamento do Merge Agent, formatada como YYYYMMDD.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpsubscriberinfo** é usado na replicação de instantâneo, na replicação transacional e na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** ou a lista de acesso à publicação da publicação podem executar **sp_helpsubscriberinfo**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
