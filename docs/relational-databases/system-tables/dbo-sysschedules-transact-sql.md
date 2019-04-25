---
title: dbo.sysschedules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs:
- TSQL
helpviewer_keywords:
- sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a1922fd8b9cdfb327186afe453fc1904d698579
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470708"
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre agendas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada na **msdb** banco de dados.  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID da agenda de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|**schedule_uid**|**uniqueidentifier**|Identificador exclusivo da agenda do trabalho. Este valor é usado para identificar uma agenda para trabalhos distribuídos.|  
|**originating_server_id**|**int**|ID do servidor mestre do qual a agenda de trabalho foi originada.|  
|**name**|**sysname (nvarchar(128))**|Nome definido pelo usuário para a agenda de trabalho. Este nome deve ser exclusivo em um trabalho.|  
|**owner_sid**|**varbinary(85)**|Microsoft Windows *security_identifier* do usuário ou grupo que possui a agenda de trabalho.|  
|**enabled**|**int**|O status da agenda de trabalho:<br /><br /> **0** = não habilitado.<br /><br /> **1** = habilitado.<br /><br /> Se o agendamento não estiver habilitado, nenhum trabalho será executado nele.|  
|**freq_type**|**int**|A frequência com que um trabalho é executado para esta agenda.<br /><br /> **1** = apenas uma vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = mensalmente, relativo ao **freq_interval**<br /><br /> **64** = executado quando o serviço do SQL Server Agent é iniciado<br /><br /> **128** = executado quando o computador estiver ocioso|  
|**freq_interval**|**int**|Dias em que o trabalho é executado. Depende do valor de **freq_type**. O valor padrão é **0**, que indica que **freq_interval** não é usado. Consulte a tabela abaixo para os valores possíveis e seus efeitos.|  
|**freq_subday_type**|**int**|Unidades para o **freq_subday_interval**. A seguir estão os valores possíveis e suas descrições.<br /><br /> <br /><br /> **1** : Na hora especificada<br /><br /> **2** : Seconds (segundos)<br /><br /> **4** : Minutes (minutos)<br /><br /> **8** : Hours (horas)|  
|**freq_subday_interval**|**int**|Número de **freq_subday_type** períodos ocorrer entre cada execução do trabalho.|  
|**freq_relative_interval**|**int**|Quando **freq_interval** ocorre em cada mês, se **freq_interval** está **32** (mensal relativo). Pode ser um dos seguintes valores:<br /><br /> **0** = **freq_relative_interval** não é usado<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = último|  
|**freq_recurrence_**<br /><br /> **factor**|**int**|Número de semanas ou meses entre execuções agendadas de um trabalho. **freq_recurrence_factor** é usado somente se **freq_type** é **8**, **16**, ou **32**. Se essa coluna contiver **0**, **freq_recurrence_factor** não é usado.|  
|**active_start_date**|**int**|Data na qual a execução de um trabalho pode começar. A data é formatada como DDMMAAAA. NULL indica a data de hoje.|  
|**active_end_date**|**int**|Data na qual a execução de um trabalho pode parar. A data é formatada como AAAAMMDD.|  
|**active_start_time**|**int**|Hora em qualquer dia entre **active_start_date** e **active_end_date** esse trabalho começa a ser executado. A hora é formatada como HHMMSS, usando um relógio de 24 horas.|  
|**active_end_time**|**int**|Hora em qualquer dia entre **active_start_date** e **active_end_date** interromperá a execução desse trabalho. A hora é formatada como HHMMSS, usando um relógio de 24 horas.|  
|**date_created**|**datetime**|Data e hora em que a agenda foi criada.|  
|**date_modified**|**datetime**|Data e hora em que a agenda foi modificada pela última vez.|  
|**version_number**|**int**|Número da versão atual da agenda. Por exemplo, se uma agenda foi modificada 10 vezes, o **número_da_versão** é 10.|  
  
|Valor de freq_type|Efeito em freq_interval|  
|-------------------------|------------------------------|  
|**1** (uma vez)|**freq_interval** não é usado (**0**)|  
|**4** (diariamente)|Cada **freq_interval** dias|  
|**8** (Semanalmente)|**freq_interval** é um ou mais das seguintes opções:<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **4** = terça-feira<br /><br /> **8** = quarta-feira<br /><br /> **16** = quinta-feira<br /><br /> **32** = sexta-feira<br /><br /> **64** = sábado|  
|**16** (mensalmente)|Sobre o **freq_interval** dia do mês|  
|**32** (mensalmente, relativo)|**freq_interval** é um dos seguintes:<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dia da semana<br /><br /> **10** = dia de fim de semana|  
|**64** (inicia quando o serviço do SQL Server Agent é iniciado)|**freq_interval** não é usado (**0**)|  
|**128** (executado quando o computador estiver ocioso)|**freq_interval** não é usado (**0**)|  
  
## <a name="see-also"></a>Confira também  
 [dbo.sysjobschedules &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
