---
title: Integration Services (SSIS) e Studio Environments | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a829fbadbf45dd5267b2297a87fc5b8833a8c807
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750438"
---
# <a name="integration-services-ssis-and-studio-environments"></a>SSIS (Integration Services) e Studio Environments
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui dois estúdios para o trabalho com [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   O[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para desenvolver os pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] exigidos por uma solução comercial. O[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fornece o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no qual você cria pacotes.  
  
-   O[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para gerenciar pacotes em um ambiente de produção.  
  
## <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 Trabalhando no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você pode executar as seguintes tarefas:  
  
-   Execute o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para criar pacotes básicos que copiam dados de uma origem para um destino.  
  
-   Criar pacotes que incluem fluxo de controle complexo, fluxo de dados, lógica baseada em eventos e registros.  
  
-   Testar e depurar pacotes usando os recursos de solução de problemas e monitoramento no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] e os recursos de depuração do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Criar configurações que atualizam as propriedades de pacotes e objetos de pacote em tempo de execução.  
  
-   Criar um utilitário de implantação que pode instalar pacotes e suas dependências em outros computadores.  
  
-   Salvar cópias de pacotes no banco de dados msdb do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], no Repositório de Pacotes do [!INCLUDE[ssIS](../includes/ssis-md.md)] e no sistema de arquivos.  
  
 Para obter mais informações sobre o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], consulte [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx).  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 O[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fornece o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que você usa para gerenciar pacotes, monitorar pacotes em execução e determinar o impacto e a linhagem de dados para objetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Trabalhando no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], você pode executar as seguintes tarefas:  
  
-   Criar pastas para organizar pacotes de modo que faça sentido para sua organização.  
  
-   Executar pacotes que são armazenados no computador local usando o utilitário Executar Pacote.  
  
-   Executar o Utilitário de Execução de Pacotes para gerar uma linha de comando a ser usada quando o utilitário de prompt de comando **dtexec** for executado (dtexec.exe).  
  
-   Importar e exportar pacotes do banco de dados msdb do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], do Repositório de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
