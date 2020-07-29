---
title: Selecionar agenda para um trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 81a0fc26bca04ee36a116d0c0c88abec417a0aa6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752525"
---
# <a name="pick-schedule-for-job"></a>Selecionar agenda para um trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa caixa de diálogo para escolher uma agenda existente para o trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
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
  
