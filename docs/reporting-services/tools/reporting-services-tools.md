---
title: Ferramentas do Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSRS, tools
- Reporting Services, tools
- components [Reporting Services]
- components [Reporting Services], about components
- Reporting Services, components
- SSRS, components
- reports [Reporting Services], tools
- SQL Server Reporting Services, components
- SQL Server Reporting Services, tools
- architecture [Reporting Services]
ms.assetid: 23d616e3-eb90-43fb-9b7a-869bd7e22e7b
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d5027e12a7cc0bfe310c4eb6b291667cfa4d0c4f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="reporting-services-tools"></a>Ferramentas do Reporting Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] contém um conjunto de ferramentas gráficas e de scripts que dão suporte ao desenvolvimento e ao uso de relatórios elaborados em um ambiente gerenciado. O conjunto de ferramentas inclui ferramentas de desenvolvimento, de configuração e de administração, além de ferramentas de visualização de relatórios. Este tópico dá uma visão geral breve de cada ferramenta do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e como ela pode ser acessada.  
  
 Para localizar uma ferramenta imediatamente, consulte [Tutorial: Como localizar e iniciar as ferramentas do Reporting Services &#40;SSRS&#41;](../../reporting-services/tools/tutorial-how-to-locate-and-start-reporting-services-tools-ssrs.md).  
  
## <a name="tools-for-report-authoring"></a>Ferramentas de criação de relatório  
 A tabela a seguir lista as ferramentas disponíveis para criação de relatórios no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Ferramenta|Description|Como acessar|  
|----------|-----------------|-------------------|  
|[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long-md.md)]|Com o [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short-md.md)], você pode criar relatórios móveis que ajustam dinamicamente o conteúdo de acordo com sua tela ou janela do navegador e se ajustam bem a qualquer tamanho de tela.<br /><br /> Crie relatórios móveis em uma superfície de design com linhas de grade e colunas ajustáveis e elementos flexíveis de relatório móvel.<br /><br /> Para obter mais informações, consulte [Criar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).|Baixe o [Publicador de Relatórios Móveis do Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=733527)|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]|Uma exploração de dados interativa e uma experiência de apresentação visual criadas para permitir que você crie e interaja com relatórios com base em modelos tabulares do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo SharePoint Navegador dom Silverlight.|  
|Designer de Relatórios|Use esta ferramenta para criar relatórios. Inclui os seguintes recursos:<br /><br /> Implantar em um servidor de relatório no modo nativo ou no modo SharePoint.<br /><br /> Hospedada no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<br /><br /> Painel de Dados do Relatório para organizar dados usados em seu relatório.<br /><br /> Exibições com guias para design e visualização do design de relatório interativo<br /><br /> Designers de consultas para ajudar a especificar os dados a serem recuperados das fontes de dados e que estão associados aos tipos de fontes de dados do [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)<br /><br /> Editor de expressão com IntelliSense para criar expressões [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que personalizam o conteúdo e a aparência dos relatórios<br /><br /> Dá suporte a itens de relatório personalizados e designers de consultas personalizados<br /><br /> <br /><br /> Para obter mais informações, consulte [Reporting Services no SQL Server Data Tools &#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|  
|Construtor de Relatórios|Use esta ferramenta para criar relatórios. Inclui os seguintes recursos:<br /><br /> Implantar em um servidor de relatório no modo nativo ou no modo SharePoint.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] Ambiente de criação parecido com o Office[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long-md.md)]<br /><br /> Capacidade de salvar itens de relatório como partes de relatório<br /><br /> Um assistente para criar mapas<br /><br /> Agregações de agregações<br /><br /> Suporte aprimorado para expressões<br /><br /> Designers de consultas para ajudar a especificar os dados a serem recuperados de uma seleção de tipos de fontes de dados internas<br /><br /> Para obter mais informações, consulte [Construtor de Relatórios no SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md).|Baixe a [versão autônoma do Construtor de Relatórios](http://go.microsoft.com/fwlink/?LinkID=219138)<br /><br /> Ou abra o Gerenciador de Relatórios/SharePoint|  
  
## <a name="tools-for-report-server-administration"></a>Ferramentas para administração do servidor de relatório  
 Um conjunto de ferramentas gráficas e de script está disponível para administrar o servidor de relatório no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. As ferramentas que você usa dependem do modo de implantação de seu servidor de relatório.  
  
### <a name="native-mode"></a>Modo nativo  
 A tabela a seguir lista as ferramentas disponíveis para administrar o servidor de relatório implantado em modo nativo.  
  
|Ferramenta|Description|Como acessar|  
|----------|-----------------|-------------------|  
|Gerenciador de Configurações do Reporting Services|Use essa ferramenta para configurar uma instalação do Reporting Services. As tarefas disponíveis incluem:<br /><br /> Configurar as instâncias locais e remotas do servidor de relatório<br /><br /> Configurar a conta de serviço do Servidor de Relatório.<br /><br /> Criar e configurar uma ou mais URLs de serviço Web.<br /><br /> Configurar a URL do Gerenciador de Relatórios<br /><br /> Criar e configurar o banco de dados do servidor de relatório.<br /><br /> Configurar uma implantação de expansão.<br /><br /> Fazer backup, restaurar ou substituir a chave simétrica usada para criptografar cadeias de conexão e credenciais armazenadas.<br /><br /> Configurar a conta de execução autônoma.<br /><br /> Configurar um servidor SMTP para entrega de email.<br /><br /> <br /><br /> Observação: o Gerenciador de Configurações do Reporting Services não ajuda a gerenciar o conteúdo do servidor de relatório, habilitar recursos adicionais ou conceder acesso ao servidor.<br /><br /> Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).|Menu Iniciar|  
|SQL Server Management Studio|Use essa ferramenta para gerenciar uma ou mais instâncias do servidor de relatório em um único ambiente, inclusive:<br /><br /> Gerenciar instâncias locais e remotas do servidor de relatório<br /><br /> Configurar propriedades do servidor de relatório<br /><br /> Modificar definições de função<br /><br /> Desativar recursos do servidor de relatório que você não está usando<br /><br /> Gerenciar trabalhos<br /><br /> Gerenciar agendas compartilhadas|Menu Iniciar|  
|SQL Server Configuration Manager|Use essa ferramenta para:<br /><br /> Iniciar e interromper os serviços do Windows do Reporting Services<br /><br /> Configurar o Relatório de Comentários do Cliente, o local do diretório de despejo e o relatório de erros<br /><br /> <br /><br /> **\*\* Aviso \*\***Não use essa ferramenta para configurar a conta de serviço. Em vez disso, use a ferramenta Configuração do Reporting Services.<br /><br /> Para obter mais informações, consulte [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).|Menu Iniciar|  
|Utilitário rsconfig|Use essa ferramenta para configurar e gerenciar a conexão do servidor de relatório com o banco de dados do servidor de relatório. Você também pode usá-lo para especificar uma conta de usuário a ser usada para processamento de relatório autônomo.<br /><br /> Para obter mais informações, consulte [Utilitários de prompt de comando do Servidor de Relatório &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Prompt de comando|  
|Utilitário rskeymgmt|Use essa ferramenta para:<br /><br /> Extrair, restaurar, criar e excluir a chave simétrica usada para criptografar dados do servidor de relatório<br /><br /> Unir instâncias do servidor de relatório em uma implantação de expansão<br /><br /> <br /><br /> Para obter mais informações, consulte [Utilitários de prompt de comando do Servidor de Relatório &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Prompt de comando|  
|Classes WMI (Instrumentação de Gerenciamento do Windows)|Use essas classes para automatizar as tarefas de configuração no Gerenciador de Configurações do Reporting Services sem precisar usar a interface gráfica do usuário.<br /><br /> Para obter mais informações, consulte [Accessing the WMI Provider Programmatically](../../reporting-services/accessing-the-wmi-provider-programmatically.md).|Script do Visual Basic|  
  
### <a name="sharepoint-integrated-mode"></a>Modo integrado do SharePoint  
 No modo do SharePoint, o Reporting Services é um aplicativo de serviço na arquitetura do SharePoint e é administrado diretamente pelo SharePoint  
  
|Ferramenta|Description|Como acessar|  
|----------|-----------------|-------------------|  
|Administração Central do SharePoint|Use a Administração Central do SharePoint para criar, consultar e gerenciar os aplicativos de serviço compartilhados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Para obter mais informações, consulte [Configuração e administração de um servidor de relatório &#40;modo do SharePoint do Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).|Navegador para a URL do site do SharePoint para a Administração Central|  
|Cmdlets do PowerShell|Use os cmdlets do PowerShell para criar, consultar e gerenciar os aplicativos de serviço compartilhados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Para obter mais informações, consulte [Cmdlets do PowerShell para o modo SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|Shell de Gerenciamento do SharePoint 2010|  
  
## <a name="tools-for-report-content-management"></a>Ferramentas para gerenciamento de conteúdo de relatório  
 Um conjunto de ferramentas gráficas e de script está disponível para gerenciamento de conteúdo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. As ferramentas que você usa dependem do modo de implantação de seu servidor de relatório.  
  
|Ferramenta|Description|Como acessar|  
|----------|-----------------|-------------------|  
|URL do serviço Web do Servidor de Relatório|Use essa ferramenta para procurar conteúdo no catálogo de relatórios em uma página de navegação de item genérica.<br /><br /> Para obter mais informações, consulte [Report Server Web Service](../../reporting-services/report-server-web-service/report-server-web-service.md).|Navegador|  
|Portal da Web|**(Apenas modo nativo)** Use essa ferramenta para administrar uma única instância do servidor de relatório em um local remoto por meio de uma conexão HTTP. É possível fazer o seguinte:<br /><br /> Exibir, pesquisar, imprimir e assinar os relatórios.<br /><br /> Criar, proteger e manter a hierarquia de pastas para organizar itens no servidor.<br /><br /> Configure a segurança baseada em função que determina o acesso a itens e operações.<br /><br /> Configurar propriedades de execução de relatório, histórico de relatórios e parâmetros de relatório.<br /><br /> Criar modelos de relatório que se conectam e recuperam dados de uma fonte de dados do Microsoft SQL Server Analysis Services ou de uma fonte de dados relacional do SQL Server.<br /><br /> Definir a segurança do item de modelo para permitir acesso a entidades específicas no modelo ou mapear entidades para relatórios de clickthrough predefinidos que você cria com antecedência.<br /><br /> Criar agendas compartilhadas e fontes de dados compartilhadas para tornar as agendas e as conexões de fonte de dados mais gerenciáveis.<br /><br /> Criar assinaturas dirigidas aos dados que distribuem relatórios para uma grande lista de destinatários.<br /><br /> Criar relatórios vinculados para reutilizar e redefinir o propósito de um relatório existente de diferentes maneiras.<br /><br /> Iniciar o Construtor de Relatórios para criar relatórios que você possa salvar e executar no servidor de relatório. Para obter mais informações, veja [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md).| Navegador  
|Utilitário RS|Essa ferramenta é um host de script que pode ser usado para executar operações de script. Use essa ferramenta para executar scripts do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que copiam dados entre os bancos de dados do servidor de relatório, publicam relatórios, criam itens em um banco de dados do servidor de relatório e outras funções. Para obter mais informações, consulte [Utilitários de prompt de comando do Servidor de Relatório &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Prompt de comando|  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de Relatório do Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Conceitos do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
