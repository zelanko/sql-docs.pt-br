---
title: Tabelas do SQL Server Agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Agent, system tables
- system tables [SQL Server], SQL Server Agent
ms.assetid: 6cb39bfd-079e-4be4-9c42-2fa234c65ce1
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f45847235f549eb80404236633111f5678f53825
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263524"
---
# <a name="sql-server-agent-tables-transact-sql"></a>Tabelas do SQL Server Agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os tópicos desta seção descrevem as tabelas do sistema que armazenam informações usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Todas as tabelas estão no esquema dbo do banco de dados msdb.  
  
## <a name="in-this-section"></a>Nesta seção  
 [dbo.sysalerts](../../relational-databases/system-tables/dbo-sysalerts-transact-sql.md)  
 Contém uma linha para cada alerta.  
  
 [dbo.syscategories](../../relational-databases/system-tables/dbo-syscategories-transact-sql.md)  
 Contém as categorias usadas pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para organizar trabalhos, alertas e operadores.  
  
 [dbo.sysdownloadlist](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)  
 Mantém a fila de instruções de download para todos os servidores de destino.  
  
 [dbo.sysjobactivity](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
 Contém informações sobre a atividade do trabalho e o status atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
 Contém informações sobre a execução de trabalhos agendados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)  
 Armazena as informações de cada trabalho agendado para ser executado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobschedules](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
 Contém informações da agenda de trabalhos a serem executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
 Armazena a associação ou a relação de um trabalho específico com um ou mais servidores de destino.  
  
 [dbo.sysjobsteps](../../relational-databases/system-tables/dbo-sysjobsteps-transact-sql.md)  
 Contém as informações de cada etapa em um trabalho a ser executado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobstepslogs](../../relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql.md)  
 Contém informações sobre logs da etapa de trabalho.  
  
 [dbo.sysnotifications](../../relational-databases/system-tables/dbo-sysnotifications-transact-sql.md)  
 Contém uma linha para cada notificação.  
  
 [dbo.sysoperators](../../relational-databases/system-tables/dbo-sysoperators-transact-sql.md)  
 Contém uma linha para cada operador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysproxies](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
 Contém informações sobre contas proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysproxylogin](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)  
 Registra quais logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão associados a cada conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysproxysubsystem](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 Registra qual subsistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é usado por cada conta proxy.  
  
 [dbo.sysschedules](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
 Contém informações sobre agendas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.syssessions](../../relational-databases/system-tables/dbo-syssessions-transact-sql.md)  
 Contém a data de início do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para cada sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Uma sessão é criada toda vez que o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado.  
  
 [dbo.syssubsystems](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 Contém informações sobre todos os subsistemas proxy disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.systargetservergroupmembers](../../relational-databases/system-tables/dbo-systargetservergroupmembers-transact-sql.md)  
 Registra quais servidores de destino estão atualmente inscritos neste grupo multisservidor.  
  
 [dbo.systargetservergroups](../../relational-databases/system-tables/dbo-systargetservergroups-transact-sql.md)  
 Registra quais grupos de servidores de destino estão atualmente inscritos neste ambiente multisservidor.  
  
 [dbo.systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
 Registra quais servidores de destino estão inscritos atualmente neste domínio de operação multisservidor.  
  
 [dbo.systaskids](../../relational-databases/system-tables/dbo-systaskids-transact-sql.md)  
 Contém um mapeamento das tarefas criadas em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para trabalhos do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] na versão atual.  
  
  
