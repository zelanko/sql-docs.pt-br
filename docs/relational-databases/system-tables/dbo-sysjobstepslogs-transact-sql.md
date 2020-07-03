---
title: dbo.sysjobstepslogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1807760e10c6a158ab2ef05162e391290e073ab4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890436"
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém o log de todas as etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que estão configuradas para gravar saída de etapa de trabalho em uma tabela. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**log_id**|**int**|ID do log de etapa de trabalho.|  
|**Façam**|**nvarchar(max)**|Conteúdo do log de etapa de trabalho.|  
|**date_created**|**datetime**|Data e hora em que o log de etapa de trabalho foi criado.|  
|**date_modified**|**datetime**|Data e hora em que o log de etapa de trabalho foi modificado pela última vez.|  
|**log_size**|**int**|Tamanho do log de etapa de trabalho em bytes.|  
|**step_uid**|**uniqueidentifier**|Identificador exclusivo da etapa de trabalho.|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_help_jobsteplog](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobsteplog](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
