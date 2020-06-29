---
title: Servidor Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3425a628b5779f8f088a6144355449fc94d988b1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439083"
---
# <a name="integration-services-ssis-server"></a>Servidor do Integration Services (SSIS)
  Depois de criar e testar pacotes no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode implantar os projetos que contêm os pacotes no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 O servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados do `SSISDB`. O banco de dados armazena os seguintes objetos: pacotes, projetos, parâmetros, permissões, propriedades de servidor e histórico operacional.  
  
 O banco de dados do `SSISDB` expõe as informações de objeto em exibições públicas que você pode consultar. O banco de dados também fornece procedimentos armazenados que você pode chamar para gerenciar os objetos.  
  
 Para poder implantar os projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você precisa criar o catálogo do `SSISDB`.  
  
 Para obter uma visão geral da funcionalidade de catálogo do SSISDB, confira [Catálogo do SSIS](ssis-catalog.md).  
  
## <a name="high-availability"></a>Alta disponibilidade  
 Como outros bancos de dados de usuários, o banco de dados `SSISDB` dá suporte a espelhamento de banco de dados e replicação. Para obter mais informações sobre espelhamento e replicação, veja [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Você também pode fornecer alta disponibilidade do SSISDB e de seu conteúdo utilizando o SSIS e grupos de disponibilidade AlwaysOn. Para obter mais informações, consulte a publicação deste blog de Matt Masson, [SSIS com AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=255873)em blogs.msdn.com.  
  
##  <a name="integration-services-server-in-sql-server-management-studio"></a><a name="ssms"></a>Integration Services servidor no SQL Server Management Studio  
 Quando você conecta a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados do `SSISDB`, vê os seguintes objetos no Pesquisador de Objetos:  
  
-   **Banco de dados SSISDB**  
  
     O `SSISDB` banco de dados é exibido sob o nó **databases** no objeto Explore. Você pode consultar as exibições e chamar os procedimentos armazenados que gerenciam o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os objetos que estão armazenados no servidor.  
  
-   **Catálogos do Integration Services**  
  
     No nó **Catálogos do Integration Services** , há pastas para projetos e ambientes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Criar o catálogo do SSIS](../create-the-ssis-catalog.md)  
  
-   [Exibir a lista de pacotes no servidor do Integration Services](view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Implantar projetos no servidor do Integration Services](../deploy-projects-to-integration-services-server.md)  
  
-   [Executar um pacote no servidor SSIS usando o SQL Server Management Studio](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog [SSIS com AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=255873)em blogs.msdn.com.  
  
  
