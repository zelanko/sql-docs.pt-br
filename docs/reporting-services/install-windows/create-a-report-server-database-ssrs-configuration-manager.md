---
title: "Criar um Banco de Dados de Servidor de Relat&#243;rio (Gerenciador de Configura&#231;&#245;es do SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servidores de relatório [Reporting Services], bancos de dados"
  - "banco de dados do servidor de relatório"
  - "bancos de dados [Reporting Services], criação"
ms.assetid: 8a3a6ffe-4001-46be-8548-94532550f6a5
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Criar um Banco de Dados de Servidor de Relat&#243;rio (Gerenciador de Configura&#231;&#245;es do SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O **Modo nativo** usa dois bancos de dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar objetos e metadados de servidor de relatório. Um banco de dados é usado para armazenamento primário e o segundo armazena dados temporários. Os bancos de dados são criados juntamente e associados por nome. Com uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão, os bancos de dados são nomeados **reportserver** e **reportservertempdb**. Coletivamente, os dois bancos de dados são referidos como o "banco de dados do servidor de relatório" ou "catálogo do servidor de relatório".  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O **Modo do SharePoint** inclui um terceiro banco de dados que é usado para metadados de alertas de dados. Os três bancos de dados são criados para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e os nomes de bancos de dados por padrão incluem uma interface gráfica de usuário que representa o aplicativo de serviço. A seguir são apresentados nomes de exemplo dos três bancos de dados do modo do SharePoint:  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
>  Não grave aplicativos que executem consultas em relação ao banco de dados do servidor de relatório. O banco de dados do servidor de relatório não é um esquema público. A estrutura da tabela pode ser alterada de uma versão para a próxima. Se você gravar um aplicativo que requeira acesso ao banco de dados do servidor de relatório, sempre use as APIs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para acessar o banco de dados do servidor de relatório.  
>   
>  A exceção a isto são as exibições do log de execução. Para obter mais informações, veja [ExecutionLog do Servidor de Relatório e a exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
## Maneiras para criar o banco de dados do servidor de relatório  
 **Modo Nativo:** você pode criar o banco de dados do servidor de relatório do modo Nativo das seguintes maneiras:  
  
-   Automaticamente: use o Assistente para Configuração do SQL Server, se você escolher a opção de instalação de configuração padrão. No Assistente de Instalação do SQL Server, é a opção **Instalar e configurar** na página Opções de Instalação do Servidor de Relatório. Caso escolha a opção **Instalar somente**, você deverá usar o Reporting Services Configuration Manager para criar o banco de dados.  
  
-   Manualmente: use a ferramenta [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Você deve criar manualmente o banco de dados do servidor de relatório se você estiver usando um [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] remoto para hospedar o banco de dados. Para obter mais informações, veja [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/create-a-native-mode-report-server-database-ssrs-configuration-manager.md).  
  
 **Modo do SharePoint:** a página de opções de Instalação do Servidor de Relatório apenas tem uma opção **Instalar somente** para o modo do SharePoint. Esta opção instala todos os arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A próxima etapa é criar pelo menos um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de uma das seguintes maneiras:  
  
-   Use a Administração Central do SharePoint para criar um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter mais informações, veja a seção “Aplicativo de serviço” de [Etapa 3: Criar um aplicativo de serviço do Reporting Services](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication).  
  
-   Use os cmdlets do PowerShell do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar um aplicativo de serviço e os bancos de dados do servidor de relatório. Para obter mais informações, confira a amostra da criação de aplicativos de serviço no tópico [Cmdlets do PowerShell para Modo do SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## Requisitos de versão do servidor de banco de dados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é usado para hospedar os bancos de dados de servidor de relatório. A instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] pode ser local ou remota. Veja a seguir as versões com suporte do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que podem ser usadas para hospedar os bancos de dados do servidor de relatório:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 A criação do banco de dados do servidor de relatório em um computador remoto requer que você configure a conexão para usar uma conta de usuário de domínio ou uma conta de serviço que tenha acesso à rede. Se você optar por usar uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere cuidadosamente quais credenciais o servidor de relatório deve usar para conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
> [!IMPORTANT]  
>  O Servidor de Relatório e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório podem estar em domínios diferentes. Para implantação na Internet, é uma prática comum usar um servidor que esteja atrás de um firewall. Se estiver configurando um servidor de relatório para acesso à Internet, use as credenciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está atrás do firewall e use IPSEC para proteger a conexão.  
  
## Requisitos de edição do servidor de banco de dados  
 Ao criar um banco de dados de servidor de relatório, esteja ciente de que nem todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem se usadas para hospedar o banco de dados. Para obter mais informações, confira a seção “Requisitos das edições do servidor de banco de dados do servidor de relatório” de [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
## Consulte também  
 [Gerenciador de Configurações do Reporting Services (modo nativo do SSRS).](http://msdn.microsoft.com/pt-br/63519ef4-e68a-42fb-9cf7-31228ea4e434)  
  
  