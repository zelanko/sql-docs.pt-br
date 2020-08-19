---
description: dbo.sysjobservers (Transact-SQL)
title: dbo.sysjobservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b4df04c6a9564c2912f39173f71735162e7dc1cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427658"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Armazena a associação ou a relação de um trabalho específico com um ou mais servidores de destino. Essa tabela é armazenada no banco de dados msdb.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|Número de identificação do trabalho.|  
|server_id|**int**|Número de identificação do servidor.|  
|last_run_outcome|**tinyint**|Resultado da última execução do trabalho:<br /><br /> **0** = falha<br /><br /> **1** = com sucesso<br /><br /> **2** = repetir<br /><br /> **3** = cancelar<br /><br /> **4** = em andamento<br /><br /> **5** = desconhecido (consulte a seção de comentários a seguir) |  
|last_outcome_ message|**nvarchar(1024)**|Mensagem associada, se houver, à coluna last_run_outcome.|  
|last_run_date|**int**|Data em que o trabalho foi executado pela última vez.|  
|last_run_time|**int**|Hora em que o trabalho foi executado pela última vez.|  
|last_run_duration|**int**|Duração pela qual o trabalho foi executado, em horas, minutos e segundos. Calculado usando a fórmula: (*horas* \* 10000) + (*minutos* \* 100) + *segundos*.|  


## <a name="remarks"></a>Comentários

Um valor acima de *4* significa que o SQL Agent não sabe o estado desse trabalho. A *last_run_outcome* é inicialmente definida como *5* quando um trabalho é criado.


## <a name="see-also"></a>Consulte Também

[SQL Server Agent tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
