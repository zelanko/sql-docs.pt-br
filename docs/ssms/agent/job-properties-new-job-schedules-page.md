---
title: Propriedades do trabalho – Novo trabalho (página Agendas)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.schedules.f1
ms.assetid: 0b03585b-a510-484d-8a63-9b32459def9c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b8cb5f6fafa2ef48b3aea31e916480e712f477af
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242263"
---
# <a name="job-properties---new-job-schedules-page"></a>Propriedades do trabalho – Novo trabalho (página Agendas)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para ver e organizar agendamentos para um trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Lista de agendas**  
Lista as agendas para esse trabalho.  
  
**Novo**  
Crie uma agenda nova. Depois de criada, a agenda é adicionada ao trabalho.  
  
**Escolher**  
Selecione uma agenda dentre as agendas existentes. Como um trabalho e uma agenda precisam ter o mesmo proprietário, essa opção não lhe permitirá escolher dentre as agendas que você tem.  
  
**Editar**  
Edite a agenda selecionada para alterar propriedades da agenda de trabalho.  
  
**Remover**  
Remova a agenda selecionada do trabalho. Se nenhum outro trabalho usar a agenda, a agenda será excluída do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
  
