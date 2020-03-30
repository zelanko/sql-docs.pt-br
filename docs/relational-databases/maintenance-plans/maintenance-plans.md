---
title: Planos de manutenção | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.AG.MAINTPLAN.LEGACY.F1
helpviewer_keywords:
- maintenance plans [SQL Server], about database maintenance plans
- maintenance plans [SQL Server], database compatibility level displayed in designer
- maintenance plans [SQL Server]
ms.assetid: 5982ca65-74fe-44e3-aef9-00a65a0db169
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f773e5188716e7f74fc75567b0c6e000607d47c9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115875"
---
# <a name="maintenance-plans"></a>Planos de manutenção
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os planos de manutenção criam um fluxo de trabalho das tarefas necessárias para garantir que o banco de dados seja otimizado, armazenado regularmente em backup e livre de inconsistências. O Assistente de Plano de Manutenção também cria os planos principais de manutenção, mas criar planos de forma manual pode oferecer uma flexibilidade bem maior.  
  
## <a name="benefits-of-maintenance-plans"></a>Benefícios de planos de manutenção  
 No [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)], os planos de manutenção criam um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que é executado por um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Os planos de manutenção podem ser executados de forma manual ou automática em intervalos agendados.  
  
 Os planos de manutenção do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] fornecem os seguintes recursos:  
  
-   Criação de fluxo de trabalho usando uma série de tarefas básicas de manutenção. É igualmente possível criar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] próprios e personalizados.  
  
-   Hierarquias conceituais. Todos os planos permitem que se criem e editem fluxos de trabalho de tarefas. As tarefas de todos os planos podem ser agrupadas em subplanos, que podem ser agendados para execução em horas diferentes.  
  
-   O suporte para planos multisservidor pode ser usado em ambientes de servidor mestre/servidor de destino.  
  
-   Suporte a histórico de plano de registro em servidores remotos.  
  
-   Suporte à Autenticação do Windows e à Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="maintenance-plan-functionality"></a>Funcionalidade de plano de manutenção  
 É possível criar planos de manutenção para executar as seguintes tarefas:  
  
-   Reorganizar os dados de páginas de índice e de dados através da recompilação de índices com um novo fator de preenchimento. A recompilação de índices com um novo fator de preenchimento garante que essas páginas de bancos de dados tenham espaços em branco e dados distribuídos igualmente. Também possibilita o crescimento mais rápido no futuro. Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
-   Compactar arquivos de dados removendo páginas vazias do banco de dados.  
  
-   Atualizar estatísticas de índices para garantir que o otimizador de consulta possua as informações atuais sobre a distribuição de valores nas tabelas, o que permite que o otimizador de consultas avalie melhor a forma de acessar os dados, já que possui mais informações sobre os dados armazenados no banco de dados. Embora as estatísticas de índice sejam atualizadas periódica e automaticamente através do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , esta opção pode forçar a atualização imediata das estatísticas.  
  
-   Executar verificações internas de consistência de páginas de dados e dados dentro do banco de dados para garantir que um problema no sistema ou software não danificou os dados.  
  
-   Fazer backup do banco de dados e dos arquivos de log de transações. É possível reter backups de bancos de dados e de logs por um período especificado, o que permite criar um histórico dos backups a serem usados caso haja necessidade de restaurar o banco de dados em uma determinada data anterior ao último backup executado. Também é possível executar backups diferenciais.  
  
-   Executar tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, o que pode ser usado para criar trabalhos que efetuem várias ações e os planos de manutenção que executem esses trabalhos.  
  
 Os resultados gerados pelas tarefas de manutenção podem ser gravados como relatórios em arquivos de texto ou como tabelas de plano de manutenção (**sysmaintplan_log** e **sysmaintplan_logdetail**) em **msdb**. Para exibir os resultados no visualizador de arquivos de log, clique com o botão direito do mouse em **Planos de Manutenção** e clique em **Exibir Histórico**.  
  
## <a name="related-tasks"></a>Related Tasks  
 Use os tópicos a seguir como introdução rápida aos planos de manutenção.  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Configure a opção **Agent XPs** de configuração do servidor para habilitar os procedimentos armazenados estendidos do SQL Server Agent.|[Opção Agent XPs de configuração do servidor](../../database-engine/configure-windows/agent-xps-server-configuration-option.md)|
|Descreve como criar um plano de manutenção usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].|[Criar um Plano de Manutenção](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)|  
|Descreve como criar um plano de manutenção usando a Superfície de Design do Plano de Manutenção.|[Criar um plano de manutenção &#40;Superfície de Design do Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/create-a-maintenance-plan-maintenance-plan-design-surface.md)|  
|Documenta a funcionalidade de plano de manutenção disponível no Pesquisador de Objetos.|[Nó de planos de manutenção &#40;Pesquisador de Objetos&#41;](../../relational-databases/maintenance-plans/maintenance-plans-node-object-explorer.md)|  
  
  
