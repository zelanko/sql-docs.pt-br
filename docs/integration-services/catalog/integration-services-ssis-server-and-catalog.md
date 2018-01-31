---
title: "Servidor e Catálogo do SSIS (Integration Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b1ba94eb985130eb7e3f8ad020756c7387df297c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-ssis-server-and-catalog"></a>Servidor e Catálogo do SSIS (Integration Services)
  Depois de criar e testar pacotes no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode implantar os projetos que contêm os pacotes no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 O servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados do **SSISDB** . O banco de dados armazena os seguintes objetos: pacotes, projetos, parâmetros, permissões, propriedades de servidor e histórico operacional.  
  
 O banco de dados do **SSISDB** expõe as informações de objeto em exibições públicas que você pode consultar. O banco de dados também fornece procedimentos armazenados que você pode chamar para gerenciar os objetos.  
  
 Para poder implantar os projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você precisa criar o catálogo do **SSISDB** .  
  
 Para obter uma visão geral da funcionalidade de catálogo do SSISDB, confira [Catálogo do SSIS](../../integration-services/catalog/ssis-catalog.md).  
  
## <a name="high-availability"></a>Alta disponibilidade  
 Como outros bancos de dados de usuários, o banco de dados **SSISDB** dá suporte a espelhamento de banco de dados e replicação. Para obter mais informações sobre espelhamento e replicação, veja [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Você também pode fornecer alta disponibilidade do SSISDB e de seu conteúdo utilizando o SSIS e grupos de disponibilidade Always On. Para obter mais informações, confira essa postagem no blog de Matt Masson, [SSIS com Always On](http://go.microsoft.com/fwlink/?LinkId=255873), em blogs.msdn.com.  
  
##  <a name="ssms"></a> Servidor do Integration Services no SQL Server Management Studio  
 Quando você conecta a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados do **SSISDB** , vê os seguintes objetos no Pesquisador de Objetos:  
  
-   **Banco de dados SSISDB**  
  
     O banco de dados do **SSISDB** aparece sob o nó **Bancos de Dados** no Pesquisador de Objetos. Você pode consultar as exibições e chamar os procedimentos armazenados que gerenciam o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os objetos que estão armazenados no servidor.  
  
-   **Catálogos do Integration Services**  
  
     No nó **Catálogos do Integration Services** , há pastas para projetos e ambientes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Exibir a lista de pacotes no servidor do Integration Services](../../integration-services/catalog/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Implantar projetos e pacotes do SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
-   [Executar pacotes do SSIS (Integration Services)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [SSIS com Always On](http://go.microsoft.com/fwlink/?LinkId=255873), em blogs.msdn.com.  
  
  
