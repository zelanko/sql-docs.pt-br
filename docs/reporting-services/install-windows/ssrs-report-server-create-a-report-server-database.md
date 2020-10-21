---
title: Criar um banco de dados de servidor de relatório, Gerenciador de Configurações | Microsoft Docs
description: O modo nativo do SQL Server Reporting Services usa dois bancos de dados relacionais do SQL Server para armazenar objetos e metadados de servidor de relatório. Um banco de dados é usado para armazenamento primário e o segundo armazena dados temporários.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.custom: seodec18
ms.date: 9/2/2020
ms.openlocfilehash: 1169c75eb349f4b997a434acc5f7e0e7cc2792f3
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935571"
---
# <a name="create-a-report-server-database-report-server-configuration-manager"></a>Criar um banco de dados do servidor de relatório, Gerenciador de Configurações do Servidor de Relatório  

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

O modo nativo do Servidor SQL [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa dois bancos de dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar objetos e metadados de servidor de relatório. Um banco de dados é usado para armazenamento primário e o segundo armazena dados temporários. 

Os bancos de dados são criados juntamente e associados por nome. Com uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão, os bancos de dados são nomeados **reportserver** e **reportservertempdb**. Coletivamente, os dois bancos de dados são chamados de **banco de dados do servidor de relatório** ou **catálogo do servidor de relatório**.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]modo do SharePoint**do SQL Server** inclui um terceiro banco de dados que é usado para metadados de alertas de dados. Os três bancos de dados são criados para cada aplicativo de serviço SSRS. Por padrão, os nomes de banco de dados incluem um GUID que representa o aplicativo de serviço. 

A seguir são apresentados nomes de exemplo dos três bancos de dados do modo do SharePoint:

- ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  

::: moniker-end
  
> [!IMPORTANT]  
> Não grave aplicativos que executem consultas em relação ao banco de dados do servidor de relatório. O banco de dados do servidor de relatório não é um esquema público. A estrutura da tabela pode ser alterada de uma versão para a próxima. Se você gravar um aplicativo que requeira acesso ao banco de dados do servidor de relatório, sempre use as APIs do SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para acessar o banco de dados do servidor de relatório.  
>
> Os modos de exibição do log de execução são exceções a essa regra. Para obter mais informações, veja [ExecutionLog do servidor de relatório e exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
## <a name="ways-to-create-the-report-server-database"></a>Maneiras para criar o banco de dados do servidor de relatório

 ### <a name="native-mode"></a>nativo
 Você pode criar o banco de dados do servidor de relatório do modo nativo das seguintes maneiras:  
  
- **Automático**. Use o Assistente de instalação do SQL Server se você escolher a opção de configuração padrão para instalação. No Assistente de Instalação do SQL Server, essa opção é **Instalar e configurar** na página **Opções de Instalação do Servidor de Relatório**. Se escolher a opção **Instalar somente**, você precisará usar o Gerenciador de Configurações do Servidor de Relatório do SQL Server para criar o banco de dados.  
  
- **Manual**. Use o SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Crie manualmente o banco de dados do servidor de relatório se você usa um [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] remoto para hospedar o banco de dados. Confira mais informações em [Criar um banco de dados de servidor de relatório no modo nativo](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
### <a name="sharepoint-mode"></a>SharePoint 
A página **Opções de Instalação do Servidor de Relatório** tem apenas uma opção para o modo do SharePoint, **Somente Instalar**. Esta opção instala todos os arquivos do SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o serviço compartilhado do SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A próxima etapa é criar pelo menos um aplicativo de serviço do SSRS de uma das seguintes maneiras:  
  
- Vá para a Administração Central do SharePoint Server para criar um aplicativo de serviço SSRS. Confira mais informações na seção **criar um aplicativo de serviço** de [Instalar o primeiro servidor de relatório no modo do SharePoint](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication).  
  
- Use os cmdlets do PowerShell do SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar um aplicativo de serviço e os bancos de dados do servidor de relatório. Para obter mais informações, confira a amostra da criação de aplicativos de serviço no tópico [Cmdlets do PowerShell para modo do SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  

::: moniker-end
  
## <a name="database-server-version-requirements"></a>Requisitos de versão do servidor de banco de dados

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é usado para hospedar os bancos de dados de servidor de relatório. A instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] pode ser local ou remota. As seguintes versões com suporte do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que podem hospedar os bancos de dados do servidor de relatório:  
::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

- Instância Gerenciada do Azure SQL

- SQL Server 2019

::: moniker-end
::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

- Microsoft SQL Server 2017  
::: moniker-end

- [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  

Se você criar o banco de dados do servidor de relatório em um computador remoto, configure a conexão para usar uma conta de usuário de domínio ou uma conta de serviço que tenha acesso à rede. Se você usar uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere quais credenciais o servidor de relatório deve usar para se conectar à instância. Para obter mais informações, confira [Configurar uma conexão de banco de dados do servidor de relatório &#40;Gerenciador de Configurações do Servidor de Relatório&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
> [!IMPORTANT]  
> O servidor de relatório e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório podem estar em domínios diferentes. Para implantação na Internet, é uma prática comum usar um servidor que esteja atrás de um firewall. 
>
> Se você configurar um servidor de relatório para acesso à Internet, use as credenciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está atrás do firewall. Proteja a conexão usando o IPSEC.  
  
## <a name="edition-requirements-for-a-database-server"></a>Requisitos de edição do servidor de banco de dados 

 Quando você cria um banco de dados de servidor de relatório, nem todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser usadas para hospedar o banco de dados. Confira mais informações em [Requisitos das edições do banco de dados do servidor de relatório](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md#edition-requirements-for-the-report-server-database) em [Recursos do Reporting Services compatíveis com as edições dele](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).  

## <a name="next-steps"></a>Próximas etapas

Leia sobre o [Gerenciador de Configurações do Servidor de Relatório](reporting-services-configuration-manager-native-mode.md).  

Mais perguntas? Faça uma pergunta no [Fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).