---
title: Criar um banco de dados de servidor de relatório (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- report server database
- databases [Reporting Services], creating
ms.assetid: 8a3a6ffe-4001-46be-8548-94532550f6a5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 638f96285f4dab2bb109353d7d648b9de8b6bb67
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952299"
---
# <a name="create-a-report-server-database--ssrs-configuration-manager"></a>Criar um Banco de Dados de Servidor de Relatório (Gerenciador de Configurações do SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **Modo nativo** usa dois bancos de dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar objetos e metadados de servidor de relatório. Um banco de dados é usado para armazenamento primário e o segundo armazena dados temporários. Os bancos de dados são criados juntamente e associados por nome. Com uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os bancos de dados são nomeados como `reportserver` e `reportservertempdb`. Coletivamente, os dois bancos de dados são referidos como o "banco de dados do servidor de relatório" ou "catálogo do servidor de relatório".  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **Modo do SharePoint** inclui um terceiro banco de dados que é usado para metadados de alertas de dados. Os três bancos de dados são criados para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e os nomes de bancos de dados por padrão incluem uma interface gráfica de usuário que representa o aplicativo de serviço. A seguir são apresentados nomes de exemplo dos três bancos de dados do modo do SharePoint:  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
>  Não grave aplicativos que executem consultas em relação ao banco de dados do servidor de relatório. O banco de dados do servidor de relatório não é um esquema público. A estrutura da tabela pode ser alterada de uma versão para a próxima. Se você gravar um aplicativo que requeira acesso ao banco de dados do servidor de relatório, sempre use as APIs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para acessar o banco de dados do servidor de relatório.  
>   
>  A exceção a isto são as exibições do log de execução. Para obter mais informações, consulte [log de execução do servidor de relatório e a exibição ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
## <a name="ways-to-create-the-report-server-database"></a>Maneiras para criar o banco de dados do servidor de relatório  
 **Modo nativo:** você pode criar o banco de dados do servidor de relatório do modo Nativo das seguintes maneiras:  
  
-   Automaticamente: use o Assistente de instalação do SQL Server se você escolher a opção de instalação de configuração padrão. No Assistente de Instalação do SQL Server, é a opção **Instalar e configurar** na página Opções de Instalação do Servidor de Relatório. Caso escolha a opção **Instalar somente** , você deverá usar o Reporting Services Configuration Manager para criar o banco de dados.  
  
-   Manualmente: use o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager. Você deve criar manualmente o banco de dados do servidor de relatório se você estiver usando um [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] remoto para hospedar o banco de dados. Para obter mais informações, consulte [Criar um banco de dados de servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 **Modo do SharePoint:** a página Opções de Instalação do Servidor de Relatório tem apenas uma opção para o modo do SharePoint, **Somente Instalar**. Esta opção instala todos os arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A próxima etapa é criar pelo menos um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de uma das seguintes maneiras:  
  
-   Use a Administração Central do SharePoint para criar um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, confira a seção "Aplicativo de serviço" da [Etapa 3: Criar um aplicativo de serviço do Reporting Services](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md#bkmk_create_serrviceapplication).  
  
-   Use os cmdlets do PowerShell do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar um aplicativo de serviço e os bancos de dados do servidor de relatório. Para obter mais informações, confira a amostra da criação de aplicativos de serviço no tópico [Cmdlets do PowerShell para Modo do SharePoint do Reporting Services](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="database-server-version-requirements"></a>Requisitos de versão do servidor de banco de dados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é usado para hospedar os bancos de dados de servidor de relatório. A instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] pode ser local ou remota. Veja a seguir as versões com suporte do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que podem ser usadas para hospedar os bancos de dados do servidor de relatório:  
  
- SQL Server 2014
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
 A criação do banco de dados do servidor de relatório em um computador remoto requer que você configure a conexão para usar uma conta de usuário de domínio ou uma conta de serviço que tenha acesso à rede. Se você optar por usar uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , considere cuidadosamente quais credenciais o servidor de relatório deve usar para conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
> [!IMPORTANT]  
>  O Servidor de Relatório e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório podem estar em domínios diferentes. Para implantação na Internet, é uma prática comum usar um servidor que esteja atrás de um firewall. Se estiver configurando um servidor de relatório para acesso à Internet, use as credenciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está atrás do firewall e use IPSEC para proteger a conexão.  
  
## <a name="database-server-edition-requirements"></a>Requisitos de edição do servidor de banco de dados  
 Ao criar um banco de dados de servidor de relatório, esteja ciente de que nem todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem se usadas para hospedar o banco de dados. Para obter mais informações, consulte a seção "requisitos de edição do servidor de banco de dados do servidor de relatório" dos [recursos com suporte nas edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Configurações do Reporting Services &#40;del&#41;](https://docs.microsoft.com/sql/sql-server/install/reporting-services-configuration-manager-native-mode)  
  
  
