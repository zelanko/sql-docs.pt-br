---
title: Eventos estendidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485c748aad8b07a5e8b92a02c03d51a82e5f362a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990700"
---
# <a name="extended-events"></a>Eventos estendidos
  Os Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm uma arquitetura altamente escalonável e configurável que permite aos usuários coletar o máximo ou o mínimo de informações, conforme necessário, para solucionar ou identificar um problema.  
  
 Você pode encontrar mais informações sobre os Eventos Estendidos na Web em [Eventos Estendidos do SQL Server](https://blogs.msdn.com/b/extended_events/).  
  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Benefícios de Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Eventos Estendidos são um sistema de monitoramento de desempenho de peso leve que usa poucos recursos de desempenho. Os Eventos Estendidos fornecem duas interfaces gráficas do usuário (**Assistente de Nova Sessão** e **Nova Sessão**) para criar, modificar, exibir e analisar os dados da sessão.  
  
## <a name="extended-events-concepts"></a>Conceitos de eventos estendidos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os Eventos Estendidos são criados com base em conceitos existentes, como um evento ou um consumidor do evento, usam conceitos de Rastreamento de Eventos para Windows e apresentam novos conceitos.  
  
 A tabela a seguir descreve os conceitos em Eventos Estendidos.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Pacotes de eventos estendidos do SQL Server](sql-server-extended-events-packages.md)|Descreve os pacotes de Eventos Estendidos que contêm objetos usados para obter e processar dados quando uma sessão de Eventos Estendidos é executada.|  
|[Destinos de eventos estendidos do SQL Server](../../database-engine/sql-server-extended-events-targets.md)|Descreve os consumidores de evento que podem receber dados durante uma sessão de evento.|  
|[Mecanismo de eventos estendidos do SQL Server](sql-server-extended-events-engine.md)|Descreve o mecanismo que implementa e gerencia uma sessão de Eventos Estendidos.|  
|[Sessões de eventos estendidos do SQL Server](sql-server-extended-events-sessions.md)|Descreve a sessão de Eventos Estendidos.|  
  
## <a name="extended-events-architecture"></a>Arquitetura de eventos estendidos  
 Os Eventos Estendidos são um sistema geral de manipulação de eventos para sistemas de servidores. A infraestrutura de Eventos Estendidos oferece suporte à correlação de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em certas condições, à correlação de dados entre sistema operacional e aplicativos de banco de dados. No último caso, a saída dos Eventos Estendidos deve ser direcionada para o ETW (Rastreamento de Eventos do Windows) a fim de correlacionar dados de evento com o sistema operacional ou os dados de evento do aplicativo.  
  
 Todos os aplicativos têm pontos de execução que são úteis dentro e fora de um aplicativo. Dentro do aplicativo, o processamento assíncrono pode ser enfileirado usando informações coletadas durante a execução inicial de uma tarefa. Fora do aplicativo, pontos de execução fornecem utilitários de monitoramento com informações sobre as características comportamentais e de desempenho do aplicativo monitorado.  
  
 O sistema Eventos Estendidos oferece suporte a dados de evento fora de um processo. Esses dados são geralmente usados por:  
  
-   Ferramentas de rastreamento, como o Rastreamento do SQL e o Monitor do Sistema.  
  
-   Ferramentas de log, como o log de eventos do Windows ou o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usuários que administram um produto ou desenvolvem aplicativos em um produto.  
  
 Os Eventos Estendidos têm os estes aspectos de design principais:  
  
-   O mecanismo Eventos Estendidos é agnóstico. Ele permite que o mecanismo associe qualquer evento a qualquer destino porque o mecanismo não é restrito ao conteúdo do evento. Para obter mais informações sobre o mecanismo Eventos Estendidos, consulte [SQL Server Extended Events Engine](sql-server-extended-events-engine.md).  
  
-   Os eventos são separados dos consumidores de evento, que são chamados *destinos* em Eventos Estendidos. Isso significa que qualquer destino pode receber qualquer evento. Além disso, qualquer evento gerado pode ser consumido automaticamente pelo destino, que pode registrar em log ou fornecer contexto de evento adicional. Para obter mais informações, consulte [SQL Server Extended Events Targets](../../database-engine/sql-server-extended-events-targets.md).  
  
-   Os eventos são distintos quanto à ação quando ocorre um evento. Portanto, qualquer ação pode ser associada a qualquer evento.  
  
-   Os predicados podem filtrar dinamicamente quando os dados de evento devem ser capturados. Isso confere flexibilidade à infraestrutura de Eventos Estendidos. Para obter mais informações, consulte [SQL Server Extended Events Packages](sql-server-extended-events-packages.md).  
  
 O mecanismo Eventos Estendidos pode gerar dados de evento de forma síncrona (e processar os dados de forma assíncrona) o que fornece uma solução flexível para manipulação de eventos. Além disso, o mecanismo Eventos Estendidos fornece os seguintes recursos:  
  
-   Uma abordagem unificada no tratamento de eventos em todo o sistema de servidor, permitindo, ao mesmo tempo, que os usuários isolem eventos específicos com a finalidade de solucionar problemas.  
  
-   Integração com e suporte às ferramentas de ETW existentes.  
  
-   Um mecanismo de tratamento de evento completamente configurável baseado no [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A capacidade de monitorar processos ativos dinamicamente com efeito mínimo sobre esses processos.  
  
-   Uma sessão de integridade de sistema padrão que é executada sem efeitos de desempenho notáveis. A sessão coleta dados do sistema que você pode usar para ajudar a solucionar problemas de desempenho. Para obter mais informações, veja [Usar a sessão system_health](use-the-ssms-xe-profiler.md).  
  
## <a name="extended-events-tasks"></a>Tarefas de eventos estendidos  
 Usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] para executar instruções DDL, exibições e funções de gerenciamento dinâmico ou exibições de catálogo [!INCLUDE[tsql](../../includes/tsql-md.md)] , é possível criar soluções para problemas simples ou complexos de eventos estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para seu ambiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Use o **Pesquisador de Objetos** para gerenciar sessões de eventos.|[Gerenciar sessões de evento no Pesquisador de Objetos](../../ssms/object/object-explorer.md)|  
|Descreve como criar uma sessão de Eventos Estendidos.|[Criar uma sessão de Eventos Estendidos](../../database-engine/create-an-extended-events-session.md)|  
|Descreve como exibir e atualizar dados de destino.|[Exibir dados de sessão de evento](../../database-engine/view-event-session-data.md)|  
|Descreve como usar as ferramentas de Eventos Estendidos para criar e gerenciar suas sessões de Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Ferramentas de eventos estendidos](extended-events-tools.md)|  
|Descreve como alterar uma sessão de Eventos Estendidos.|[Alterar uma sessão de Eventos Estendidos](alter-an-extended-events-session.md)|  
|Descreve como copiar ou exportar dados de destino.|[Copiar ou exportar dados de destino](../../database-engine/copy-or-export-target-data.md)|  
|Descreve como modificar sua exibição de resultados de rastreamento para personalizar como você deseja analisar seus dados.|[Modificar a visualização dos resultados de rastreamento](../../database-engine/modify-the-trace-results-view.md)|  
|Descreve como obter informações sobre os campos associados aos eventos.|[Obter os campos de todos os eventos](../../database-engine/get-the-fields-for-all-events.md)|  
|Descreve como descobrir quais eventos estão disponíveis nos pacotes registrados.|[Exibir os eventos de pacotes registrados](../../database-engine/view-the-events-for-registered-packages.md)|  
|Descreve como determinar quais destinos de Eventos Estendidos estão disponíveis nos pacotes registrados.|[Exibir os destinos dos Eventos Estendidos de pacotes registrados](../../database-engine/view-the-extended-events-targets-for-registered-packages.md)|  
|Descreve como exibir os eventos e as ações dos Eventos Estendidos que são equivalentes a cada evento de Rastreamento do SQL e suas colunas associadas.|[Exibir os Eventos Estendidos equivalentes às classes de rastreamento de eventos do SQL](view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Descreve como localizar os parâmetros que você pode definir para o uso do argumento ADD TARGET em CREAT EVENT SESSION ou ALTER EVENT SESSION.|[Obter os parâmetros configuráveis para o argumento ADD TARGET](../../database-engine/get-the-configurable-parameters-for-the-add-target-argument.md)|  
|Descreve como converter um script existente de Rastreamento do SQL em uma sessão de Eventos Estendidos.|[Converter um script existente de Rastreamento do SQL em uma sessão de Eventos Estendidos](convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Descreve como determinar quais consultas estão mantendo o bloqueio, o plano da consulta e a pilha [!INCLUDE[tsql](../../includes/tsql-md.md)] no momento em que o bloqueio foi realizado.|[Determinar quais consultas estão mantendo bloqueios](determine-which-queries-are-holding-locks.md)|  
|Descreve como identificar a origem de bloqueios que estão obstruindo o desempenho do banco de dados.|[Localizar os objetos que detêm a maioria dos bloqueios](find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Descreve como usar os Eventos Estendidos com o Rastreamento de Eventos do Windows para monitorar a atividade do sistema.|[Monitorar a atividade do sistema usando Eventos Estendidos](monitor-system-activity-using-extended-events.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos da Camada de Dados](../data-tier-applications/data-tier-applications.md)   
 [Suporte ao DAC para objetos e versões do SQL Server](../data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [Implantar um aplicativo da camada de dados](../data-tier-applications/deploy-a-data-tier-application.md)   
 [Monitorar aplicativos da camada de dados](../data-tier-applications/monitor-data-tier-applications.md)   
 [Exibições de gerenciamento dinâmico de eventos estendidos](../views/views.md)   
 [Exibições do catálogo de eventos estendidos &#40;Transact-SQL&#41;] (~/relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql  
  
  
