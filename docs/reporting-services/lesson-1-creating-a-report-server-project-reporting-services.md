---
title: 'Lição 1: Criar um projeto do Servidor de Relatório | Microsoft Docs'
description: Nesta lição, você criará um projeto do servidor de relatório e um arquivo de definição de relatório (.rdl) usando o Designer de Relatórios.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6c4ed5c985340e45b46b664dc4b6a53ff70f1b1a
ms.sourcegitcommit: 83e5cfd2654233befd95e3ff37de936f9dc8549c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89468341"
---
# <a name="lesson-1-create-a-report-server-project-reporting-services"></a>Lição 1: Criar um projeto do Servidor de Relatório (Reporting Services)

Nesta lição, você criará um *projeto do servidor de relatórios* e um arquivo de *definição de relatório (.rdl)* no *Designer de Relatórios*.

> [!NOTE]
> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] é um ambiente do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para criar soluções de business intelligence. O SSDT contém um ambiente de autoria do Designer de Relatórios, em que você pode abrir, modificar, visualizar, salvar e implantar [!INCLUDE[ssrsnoversion_md](../includes/ssrsnoversion-md.md)] definições de relatório paginados, fontes de dados compartilhados, conjuntos de dados compartilhados e partes de relatório.

Criar relatórios com o Designer de Relatórios significa que você cria um projeto do servidor de relatório que contém os arquivos de relatórios e outros arquivos de recursos usados pelos relatórios.

## <a name="to-create-a-report-server-project"></a>Para criar um projeto do servidor de relatórios
  
1. No menu **Arquivo**, selecione **Novo** > **Projeto**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
2. Na coluna mais à esquerda em **Instalado**, selecione **Reporting Services**. Em alguns casos, talvez ele esteja no grupo **Business Intelligence**.

    ![select-report-server-project-template](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

    > [!IMPORTANT]
    > No VS, se você não vir o Reporting Services na coluna esquerda, adicione o Designer de Relatórios ao instalar a carga de trabalho do SSDT. No menu **Ferramentas**, selecione **Obter Ferramentas e Funcionalidades...**  e selecione **SQL Server Data Tools** nas cargas de trabalho exibidas. Se você não vir os objetos de serviços de relatórios na coluna central, adicione as extensões do Reporting Services. No menu **Ferramentas**, selecione **Extensões e Atualizações** > **Online**. Na coluna central, selecione **Projetos do Microsoft Reporting Services** > **Baixar** nas extensões exibidas. Para SSDT, confira [Baixar o SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md). No Visual Studio 2019, se as etapas anteriores não funcionaram, tente instalar a [extensão do Projeto do Microsoft Reporting Service](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio).


3. Selecione o ícone **Projeto do Servidor de Relatório** &nbsp;&nbsp;![ssrs_ssdt_report_server_project](media/ssrs-ssdt-report-server-project.png) &nbsp;&nbsp;na coluna central da caixa de diálogo **Novo Projeto**.

4. Na caixa de texto **Nome**, digite "Tutorial" como o nome do projeto. Por padrão, a caixa de texto **Local** exibe o caminho para a pasta "Documentos\Visual Studio 20xx\Projetos\". O Designer de Relatórios cria a pasta Tutorial nesse caminho e cria o projeto do Tutorial nessa pasta. Se o projeto não pertencer a uma solução VS, então o VS também cria um arquivo de solução (.sln).

5. Selecione **OK** para criar o projeto. O projeto Tutorial é exibido no painel **Gerenciador de Soluções** à direita.
  
## <a name="creating-a-report-definition-file-rdl"></a>Criar um arquivo de definição de relatório (RDL)  
  
1. No painel **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Relatórios**. Se você não vir o painel **Gerenciador de Soluções**, selecione o menu **Exibir** > **Gerenciador de Soluções**.

2. Selecione **Adicionar** > **Novo Item**.

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)

3. Na janela **Adicionar Novo Item**, selecione o ícone **Relatório**.

4. Digite "Pedidos de Vendas.rdl" na caixa de texto **Nome**.

5. Selecione o botão **Adicionar** no canto inferior direito da caixa de diálogo **Adicionar Novo Item** para concluir o processo. O Designer de Relatórios abre e exibe o novo arquivo do relatório de Pedido de Vendas no modo de exibição de Design.

    ![ssrs-ssdt-01-new-report-designer](media/ssrs-ssdt-01-new-report-designer.png)

## <a name="next-steps"></a>Próximas etapas

Até agora, você criou o projeto de relatório do Tutorial e o relatório Pedidos de Vendas. Nas próximas lições, você aprenderá como:

- Configura uma fonte de dados para o relatório.
- Criar um conjunto de dados a partir da fonte de dados.
- Criar e formatar o layout do relatório.

Continue na [Lição 2: especificar informações da conexão &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).
