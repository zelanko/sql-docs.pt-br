---
title: Escolher um agente para o trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cbae4854bff8396f64e04a662d0e2b48548934b7
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="pick-schedule-for-job"></a>Selecionar agenda para um trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa caixa de diálogo para escolher uma agenda existente para o trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Agendas disponíveis**  
Exibe as agendas disponíveis para esse trabalho. Como um trabalho e uma agenda precisam ter o mesmo proprietário, essa lista incluirá somente as agendas de propriedade do proprietário do trabalho.  
  
**Nome**  
Exibe o nome da agenda.  
  
**Enabled**  
Selecionado se a agenda estiver habilitada.  
  
**Descrição**  
Descreve as condições em que a agenda executa o trabalho.  
  
**Trabalhos na agenda**  
Exibe os números de trabalhos anexados à agenda. Clique em um número para exibir as propriedades do trabalho.  
  
**Propriedades**  
Lança a caixa de diálogo **Propriedades da Agenda do Trabalho** na qual você pode exibir informações sobre a agenda.  
  
## <a name="see-also"></a>Consulte Também  
[Criar e anexar agendas para trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
