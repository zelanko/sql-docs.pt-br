---
title: Exibir resultados da política de integridade de recursos (Utilitário do SQL Server) | Microsoft Docs
description: Saiba como usar SQL Server Management Studio para exibir resultados da política de integridade de recursos do Utilitário do SQL Server para instâncias de SQL Server e aplicativos da camada de dados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a3ec26ba8988f36e3deac88373a932ef377f8d59
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810018"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>Exibir resultados da política de integridade de recursos (Utilitário do SQL Server)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use o painel (dashboard) do Utilitário do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir parâmetros de recursos do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de aplicativos da camada de dados. Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

##  <a name="SSMSProcedure"></a>

### <a name="view-sql-server-utility-resource-health-policy-results"></a>Exibir resultados da política de integridade de recursos do Utilitário do SQL Server.  

1. No SSMS ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]), selecione **Exibir** e depois **Gerenciador do Utilitário** para exibir o painel de navegação do Gerenciador do Utilitário. Para exibir o painel de conteúdo, selecione **Exibir** e depois **Conteúdo do Gerenciador do Utilitário**.  

2. No painel de navegação, selecione ![conectar ao utilitário](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**Conectar ao Utilitário**. Se você não criou um UCP (ponto de controle do utilitário) ou se não inscreveu instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou aplicativos da camada de dados no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

3. Clique no nó do UCP para exibir dados de resumo das instâncias gerenciadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos da camada de dados (clique com o botão direito do mouse para atualizar). Dados do painel são exibidos no painel de conteúdo.  

4. Clique no nó das **Instâncias Gerenciadas** para exibir os dados da exibição de lista das instâncias gerenciadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (clique com o botão direito do mouse para atualizar). Dados de exibição de lista são exibidos no painel de conteúdo.  

5. Clique no nó de **Aplicativos da Camada de Dados Implantados** para exibir os dados da exibição de lista dos aplicativos da camada de dados (clique com o botão direito do mouse para atualizar). Dados de exibição de lista são exibidos no painel de conteúdo.  

## <a name="see-also"></a>Consulte Também

- [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)
- [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130))
- [Detalhes da instância gerenciada &#40;Utilitário do SQL Server&#41;](./utility-explorer-f1-help.md)
- [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))