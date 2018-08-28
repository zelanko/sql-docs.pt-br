---
title: Introdução ao SQL Server Management Studio para BI | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae76873ce9156dd62478f7088d383ddff2c42b7d
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42775572"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>Introdução ao SQL Server Management Studio para Business Intelligence
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para acessar, configurar, gerenciar e administrar o [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], use o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Embora essas três tecnologias de business intelligence dependam do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], as tarefas administrativas associadas a cada tecnologia são ligeiramente diferentes.  
  
> [!NOTE]  
> Para criar e modificar soluções [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , use [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)], não [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)] é um ambiente de desenvolvimento baseado no [!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>Gerenciando as soluções do Analysis Services com o SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite gerenciar objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] , como executar backups e processar objetos.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] fornece um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script no qual é possível desenvolver e salvar scripts gravados em MDX (expressões MDX), DMX (extensões DMX) e XMLA (XML for Analysis). Use os projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script para executar tarefas de gerenciamento ou recriar objetos, como bancos de dados e cubos, nas instâncias do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] . Por exemplo, você pode desenvolver um script XMLA em um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script que cria novos objetos diretamente em uma instância existente do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] . Os projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script podem ser salvos como parte de uma solução e integrados ao controle do código fonte.  
  
Para obter mais informações sobre como usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consulte [Desenvolvimento e implementação usando o SQL Server Management Studio](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>Gerenciando as soluções do Integration Services com o SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite usar o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para gerenciar pacotes e monitorar os pacotes em execução. Você também pode usar o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para organizar os pacotes em pastas, executar pacotes, importar e exportar pacotes, migrar pacotes DTS e atualizar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>Gerenciando os projetos do Reporting Services com o SQL Server Management Studio  
Use o SQL Server Management Studio para habilitar recursos do Reporting Services, administrar o servidor e os bancos de dados e gerenciar funções e trabalhos.  
  
Você pode gerenciar agendas compartilhadas usando a pasta Agendas Compartilhadas e gerenciar bancos de dados do servidor de relatórios (ReportServer, ReportServerTempdb). Você também pode criar uma função RSExecRole no banco de dados Mestre do sistema ao mover um banco de dados de servidor de relatórios para um Mecanismo de Banco de Dados do SQL Server novo ou diferente ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)]). Para obter mais informações sobre essas tarefas, consulte os seguintes tópicos:  
  
-   [Tópicos de instruções do Management Studio](http://msdn.microsoft.com/60685458-9108-47bf-820a-5e7db454d408)  
  
-   [Administrando um banco de dados do servidor de relatórios](../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)  
  
-   [Como criar o RSExecRole](../reporting-services/security/create-the-rsexecrole.md)  
  
Você também pode gerenciar o servidor habilitando e configurando vários recursos, definindo padrões de servidor e gerenciando funções e trabalhos. Para obter mais informações sobre essas tarefas, consulte os seguintes tópicos:  
  
-   [Como definir propriedades do servidor de relatório (Management Studio)](http://msdn.microsoft.com/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)  
  
-   [Como criar, excluir ou modificar uma função (Management Studio)](http://msdn.microsoft.com/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)  
  
-   [Habilitando e desabilitando impressão do lado do cliente para Reporting Services](http://msdn.microsoft.com/0e709c96-7517-4547-8ef6-5632f8118524)  
  
## <a name="see-also"></a>Consulte Também  
[Desenvolvimento e implementação usando o SQL Server Data Tools](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
[Reporting Services no SQL Server Data Tools](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
