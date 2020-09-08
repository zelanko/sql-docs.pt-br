---
description: sysdbmaintplan_jobs (Transact-SQL)
title: sysdbmaintplan_jobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_jobs
- sysdbmaintplan_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_jobs system table
ms.assetid: bc65cd70-6ef2-4c17-be11-877ecf4efe50
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ab3398bdf0c258a5997ce64d48db781234059bf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517620"
---
# <a name="sysdbmaintplan_jobs-transact-sql"></a>sysdbmaintplan_jobs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta tabela é incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para preservar informações existentes de instâncias atualizadas de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não altera o conteúdo dessa tabela. Essa tabela é armazenada no banco de dados **msdb** .  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|ID do plano de manutenção do banco de dados.|  
|**job_id**|**uniqueidentifier**|ID de um trabalho associado ao plano de manutenção do banco de dados.|  
  
  
