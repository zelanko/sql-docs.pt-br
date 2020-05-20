---
title: dbo. sysjobstepslogs (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 8d59f8aa3bef0b2f8f021c4661d8815485ca32e1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82806803"
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  
