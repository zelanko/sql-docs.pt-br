---
title: "Exibir resultados da política de integridade de recursos (Utilitário do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b640be4a2da49c03c06b69b9e7d9c2ea4971e769
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>Exibir resultados da política de integridade de recursos (Utilitário do SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use o painel do Utilitário no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir parâmetros de recursos do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos da camada de dados. Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>Exibir resultados da política de integridade de recursos do Utilitário do SQL Server.  
  
1.  No SSMS ( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ), clique em **Exibir**e em **Gerenciador do Utilitário** para exibir o painel de navegação do Gerenciador do Utilitário. Para exibir o painel de conteúdo, clique em **Exibir**e em **Conteúdo do Gerenciador do Utilitário**.  
  
2.  No painel de navegação, clique em ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**Conectar ao Utilitário**. Se você não criou um UCP (ponto de controle do utilitário) ou se não inscreveu instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou aplicativos da camada de dados no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
3.  Clique no nó do UCP para exibir dados de resumo das instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de aplicativos da camada de dados (clique com o botão direito do mouse para atualizar). Dados do painel são exibidos no painel de conteúdo.  
  
4.  Clique no nó **Instâncias Gerenciadas** para exibir dados de exibição de lista das instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (clique com o botão direito do mouse para atualizar). Dados de exibição de lista são exibidos no painel de conteúdo.  
  
5.  Clique no nó **Aplicativos da Camada de Dados Implantados** para exibir dados da exibição de lista dos aplicativos da camada de dados (clique com o botão direito do mouse para atualizar). Dados de exibição de lista são exibidos no painel de conteúdo.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)   
 [Detalhes de instâncias gerenciadas &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)   
 [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)  
  
  
