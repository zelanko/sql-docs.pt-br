---
description: Ferramentas de desenvolvimento e gerenciamento do SSIS (Integration Services)
title: Ferramentas de desenvolvimento e gerenciamento | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fa32eb175339d3fa02afdf41e0c90471a7ef8ee5
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193878"
---
# <a name="integration-services-ssis-development-and-management-tools"></a>Ferramentas de desenvolvimento e gerenciamento do SSIS (Integration Services)

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui dois estúdios para trabalhar com pacotes:  
  
-   O[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para desenvolver os pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] exigidos por uma solução comercial. O[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fornece o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no qual você cria pacotes.  
  
-   O[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para gerenciar pacotes em um ambiente de produção.  
  
## <a name="sql-server-data-tools"></a>Ferramentas de dados do SQL Server  
 Trabalhando no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você pode executar as seguintes tarefas:  
  
-   Execute o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para criar pacotes básicos que copiam dados de uma origem para um destino.  
  
-   Criar pacotes que incluem fluxo de controle complexo, fluxo de dados, lógica baseada em eventos e registros.  
  
-   Testar e depurar pacotes usando os recursos de solução de problemas e monitoramento no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] e os recursos de depuração do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Criar configurações que atualizam as propriedades de pacotes e objetos de pacote em tempo de execução.  
  
-   Criar um utilitário de implantação que pode instalar pacotes e suas dependências em outros computadores.  
  
-   Salvar cópias de pacotes no banco de dados msdb do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], no Repositório de Pacotes do [!INCLUDE[ssIS](../includes/ssis-md.md)] e no sistema de arquivos.  
  
 Para obter mais informações sobre o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], consulte [SQL Server Data Tools](/previous-versions/sql/sql-server-data-tools/hh272686(v=vs.103)).  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 O[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fornece o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que você usa para gerenciar pacotes, monitorar pacotes em execução e determinar o impacto e a linhagem de dados para objetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Trabalhando no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], você pode executar as seguintes tarefas:  
  
-   Criar pastas para organizar pacotes de modo que faça sentido para sua organização.  
  
-   Executar pacotes que são armazenados no computador local usando o utilitário Executar Pacote.  
  
-   Executar o Utilitário de Execução de Pacotes para gerar uma linha de comando a ser usada quando o utilitário de prompt de comando **dtexec** for executado (dtexec.exe).  
  
-   Importar e exportar pacotes do banco de dados msdb do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], do Repositório de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)].