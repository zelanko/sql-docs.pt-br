---
title: dbo. sysschedules (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: cbf570a09f3316172a60206730b91644cc603f0b
ms.sourcegitcommit: 4bba3c8e3360bcbe269819d61f8898d0ad52c6e3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79090572"
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre agendas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no banco de dados **msdb** .  
  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID da agenda de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|**schedule_uid**|**uniqueidentifier**|Identificador exclusivo da agenda do trabalho. Este valor é usado para identificar uma agenda para trabalhos distribuídos.|  
|**originating_server_id**|**int**|ID do servidor mestre do qual a agenda de trabalho foi originada.|  
|**name**|**sysname (nvarchar (128))**|Nome definido pelo usuário para a agenda de trabalho. Este nome deve ser exclusivo em um trabalho.|  
|**owner_sid**|**varbinary(85)**|O Microsoft Windows *security_identifier* do usuário ou grupo que possui a agenda de trabalho.|  
|**Habilitado**|**int**|O status da agenda de trabalho:<br /><br /> **0** = não habilitado.<br /><br /> **1** = habilitado.<br /><br /> Se o agendamento não estiver habilitado, nenhum trabalho será executado nele.|  
|**freq_type**|**int**|A frequência com que um trabalho é executado para esta agenda.<br /><br /> **1** = somente uma vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = mensalmente, em relação a **freq_interval**<br /><br /> **64** = é executado quando o serviço de SQL Server Agent é iniciado<br /><br /> **128** = é executado quando o computador está ocioso|  
|**freq_interval**|**int**|Dias em que o trabalho é executado. Depende do valor de **freq_type**. O valor padrão é **0**, o que indica que **freq_interval** não é usado. Consulte a tabela abaixo para obter os possíveis valores e seus efeitos.|  
|**freq_subday_type**|**int**|Unidades para o **freq_subday_interval**. A seguir estão os possíveis valores e suas descrições.<br /><br /> <br /><br /> **1** : na hora especificada<br /><br /> **2** : segundos<br /><br /> **4** : minutos<br /><br /> **8** : horas|  
|**freq_subday_interval**|**int**|Número de períodos de **freq_subday_type** a ocorrer entre cada execução do trabalho.|  
|**freq_relative_interval**|**int**|Quando **freq_interval** ocorrer em cada mês, se **freq_type** for **32** (relativo mensal). Pode ser um dos seguintes valores:<br /><br /> **0** = **freq_relative_interval** não é usado<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = última|  
|**freq_recurrence_**<br /><br /> **multi-fator**|**int**|Número de semanas ou meses entre execuções agendadas de um trabalho. **freq_recurrence_factor** será usado somente se **freq_type** for **8**, **16**ou **32**. Se esta coluna contiver **0**, **freq_recurrence_factor** não será usado.|  
|**active_start_date**|**int**|Data na qual a execução de um trabalho pode começar. A data é formatada como DDMMAAAA. NULL indica a data de hoje.|  
|**active_end_date**|**int**|Data na qual a execução de um trabalho pode parar. A data é formatada como AAAAMMDD.|  
|**active_start_time**|**int**|Hora em qualquer dia entre **active_start_date** e **active_end_date** o trabalho começa a ser executado. A hora é formatada como HHMMSS, usando um relógio de 24 horas.|  
|**active_end_time**|**int**|Hora em qualquer dia entre **active_start_date** e **active_end_date** que o trabalho para de ser executado. A hora é formatada como HHMMSS, usando um relógio de 24 horas.|  
|**date_created**|**datetime**|Data e hora em que a agenda foi criada.|  
|**date_modified**|**datetime**|Data e hora em que a agenda foi modificada pela última vez.|  
|**version_number**|**int**|Número da versão atual da agenda. Por exemplo, se uma agenda tiver sido modificada 10 vezes, a **version_number** será 10.|  
  
|Valor de freq_type|Efeito em freq_interval|  
|-------------------------|------------------------------|  
|**1** (uma vez)|**freq_interval** não é usado (**0**)|  
|**4** (diário)|A cada **freq_interval** dias|  
|**8** (semanal)|**freq_interval** é um ou mais dos seguintes:<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **4** = terça-feira<br /><br /> **8** = quarta-feira<br /><br /> **16** = quinta-feira<br /><br /> **32** = sexta-feira<br /><br /> **64** = sábado|  
|**16** (mensal)|No **freq_interval** dia do mês|  
|**32** (mensal, relativo)|**freq_interval** é um dos seguintes:<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dia da semana<br /><br /> **10** = dia do fim de semana|  
|**64** (inicia quando SQL Server Agent serviço é iniciado)|**freq_interval** não é usado (**0**)|  
|**128** (é executado quando o computador está ocioso)|**freq_interval** não é usado (**0**)|  
  
## <a name="see-also"></a>Confira também  
 [dbo. sysjobschedules &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
