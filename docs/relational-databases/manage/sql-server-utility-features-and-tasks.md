---
title: Recursos e tarefas do Utilitário do SQL Server | Microsoft Docs
description: Familiarize-se com o Utilitário do SQL Server. Saiba mais sobre seus recursos e descubra como usá-lo para monitorar um ambiente do SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9f37e62285ffcd3623bd1a26609466556e07634c
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810412"
---
# <a name="sql-server-utility-features-and-tasks"></a>Recursos e tarefas do Utilitário do SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisam gerenciar seu ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um todo. Isso é abordado nesta versão por meio do conceito de gerenciamento de aplicativo e multisservidor do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="benefits-of-the-sql-server-utility"></a>Benefícios do Utilitário do SQL Server  
 O Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modela as entidades relacionadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de uma organização em uma exibição unificada. O Gerenciador do Utilitário e os pontos de vista do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no SSMS ( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ) fornecem aos administradores uma visão holística da integridade dos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que funciona como um UCP (ponto de controle do utilitário). A combinação de dados resumidos e detalhados apresentada no UCP para políticas de subutilização e de superutilização, e para uma variedade de parâmetros chave, permite que oportunidades de consolidação de recursos e de superutilização de recursos sejam identificadas facilmente. As políticas de integridade são configuráveis e podem ser ajustadas para alterar os limites inferior e superior da utilização de recursos. É possível alterar as políticas de monitoramento globais ou configurar políticas de monitoramento individuais para cada entidade gerenciada no Utilitário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="getting-started-with-sql-server-utility"></a><a name="typical_scenarios"></a> Introdução ao Utilitário do SQL Server  
 O cenário do usuário típico começa com a criação de um ponto de controle de utilitário que estabelece o ponto de raciocínio central para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. O UCP fornece uma exibição consolidada da integridade de recurso coletada de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Depois que o UCP é criado, você inscreve as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de forma que elas possam ser gerenciadas pelo UCP.  
  
 Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativo da camada de dados gerenciado pelo Utilitário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser monitorado com base nas definições da política global ou com base nas definições de políticas individuais.  
  
## <a name="related-tasks"></a>Related Tasks  
 Use os tópicos a seguir como introdução rápida ao utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Descrição|Tópico|  
|-|-|  
|Descreve considerações para configurar um servidor para executar conjuntos de coleta do utilitário e não utilitário na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Considerações sobre a execução de Conjuntos de Coleta do Utilitário e que não são do Utilitário na mesma instância do SQL Server](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|Descreve como criar um ponto de controle do utilitário do SQL Server.|[Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|Descreve como se conectar a um utilitário do SQL Server.|[Conectar a um Utilitário do SQL Server](../../relational-databases/manage/connect-to-a-sql-server-utility.md)|  
|Descreve como associar uma instância do SQL Server com um Ponto de Controle de Utilitário.|[Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|Descreve como usar o Gerenciador do Utilitário para gerenciar o utilitário do SQL Server.|[Usar o Gerenciador do Utilitário para gerenciar o Utilitário do SQL Server](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|Descreve como monitorar instâncias do SQL Server no Utilitário do SQL Server.|[Monitorar instâncias do SQL Server no Utilitário do SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|Descreve como exibir resultados da política de integridade de recursos.|[Exibir resultados da política de integridade de recursos &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)|  
|Descreve como modificar uma definição de política de integridade de recursos.|[Modificar uma definição de política de integridade de recursos &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|Descreve como configurar o data warehouse de UCP.|[Configurar o data warehouse do ponto de controle do utilitário &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|Descreve como configurar políticas de integridade de utilitário.|[Configurar políticas de integridade &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)|  
|Descreve como ajustar a atenuação em políticas de utilização da CPU.|[Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|Descreve como remover uma instância do SQL Server de um UCP.|[Remover uma instância do SQL Server do Utilitário do SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|Descreve como alterar a conta proxy para o coletor de dados do utilitário em uma instância gerenciada do SQL Server.|[Alterar a conta proxy para o conjunto de coleta do utilitário em uma instância gerenciada do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|Descreve como mover um UCP de uma instância do SQL Server para outra.|[Mover um UCP de uma instância do SQL Server para outra &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|Descreve como remover um UCP.|[Remover um ponto de controle do utilitário &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/remove-a-utility-control-point-sql-server-utility.md)|  
|Descreve como solucionar problemas do utilitário do SQL Server.|[Solucionar problemas do Utilitário do SQL Server](/previous-versions/sql/sql-server-2016/ee210592(v=sql.130))|  
|Descreve como solucionar problemas de integridade de recursos do SQL Server.|[Solucionar problemas de integridade de recursos do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|Links para tópicos da Ajuda F1 do UtilityExplorer.|[Ajuda de F1 do Gerenciador do Utilitário](../../relational-databases/manage/utility-explorer-f1-help.md)|  
  
