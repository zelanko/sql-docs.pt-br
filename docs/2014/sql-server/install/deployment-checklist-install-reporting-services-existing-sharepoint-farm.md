---
title: 'Lista de verificação de implantação: Instalar Reporting Services em um farm existente do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 436b4c3d-3f2f-464a-be7e-5c051d9ffb8f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e7a66be0d4e002643ffe1c72ce8c44aa50f61c0e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952620"
---
# <a name="deployment-checklist-install-reporting-services-into-an-existing-sharepoint-farm"></a>Lista de verificação de implantação: Instalar o Reporting Services em um farm existente do SharePoint
  Os servidores de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint podem ser instalados em um novo farm do SharePoint ou em um farm existente do SharePoint. Este tópico descreve os cenários possíveis e as práticas recomendadas para a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um farm existente do SharePoint.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de executar Setup.exe, examine as seguintes informações:  
  
|Etapa|Link|  
|----------|----------|  
|Crie ou identifique as contas usadas em uma implantação de servidor de relatório. Você deve ter uma conta de serviço para o serviço de Servidor de Relatório e credenciais para conectar-se ao banco de dados de servidor de relatório||  
|Decida sobre uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o banco de dados do servidor de relatório. Você pode usar uma instância local ou remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve escolher uma instância que esteja em um computador que tenha a capacidade de memória para acomodar seus relatórios.||  
|(Opcional) Localize o nome do servidor SMTP ou o gateway que fornece serviço de email à sua organização, se desejar usar email do servidor de relatório em assinaturas|[Configurar um servidor de relatório para entrega &#40;de email Configuration Manager do SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)|  
|Observação: Se você estiver atualizando um computador de uma versão CTP anterior [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e tiver feito alterações personalizadas nos arquivos de configuração, será necessário fazer as mesmas alterações nos arquivos de configuração, seguindo a atualização para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os arquivos afetados são **Web. config** e **Client. config**.||  
  
## <a name="installation-scenarios"></a>Cenários de instalação  
 A tabela a seguir descreve os cenários possíveis durante a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um farm existente do SharePoint. O modo local permite que os relatórios sejam renderizados localmente a partir da biblioteca de documentos do SharePoint, sem integração com um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint é necessário, mas um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não é. Para obter mais informações sobre o modo local, consulte [Modo Local versus Os relatórios do modo conectado no visualizador &#40;de relatórios Reporting Services no&#41;modo do SharePoint ](../../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md) e [onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
|Iniciando a configuração|Fluxo de trabalho|Editando a configuração|Comentários|  
|----------------------------|--------------|--------------------------|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] no modo Local|Instalação|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]no modo conectado.||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] no modo conectado|Atualização in-loco|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]no modo conectado.||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] no modo conectado|Migração|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]no modo conectado.||  
  
## <a name="installation-and-in-place-upgrade-checklist"></a>Lista de verificação de atualização e instalação in loco  
 A tabela a seguir resume as etapas, as ferramentas e as informações que você deve examinar e usar para a instalação:  
  
|Etapa|Link|  
|----------|----------|  
|**Instalação e configuração inicial**||  
|Instale o suplemento do SharePoint em todos os computadores WFE (front-end da Web).|[Adicionar um front-end da Web do Reporting Services a um farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Instalar o SQL Server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services e o mecanismo de banco de dados.|[Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Crie pelo menos um aplicativo do serviço SSRS e configure a associação do aplicativo de serviço.|Consulte a seção "aplicativo de serviço" em [instalar Reporting Services modo do SharePoint para sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|**Configuração adicional**||  
|Adicione tipos de conteúdo do SSRS à biblioteca de documentos.|[Adicionar tipos de conteúdo do servidor de relatório &#40;a uma biblioteca Reporting Services no modo integrado do SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)|  
|Provisione o SQL Server Agent|[Provisionar assinaturas e alertas para aplicativos de serviço SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)|  
|Defina as configurações de email para o aplicativo de serviço.|[Configurar o email para um serviço de aplicativo do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|Configure o c2WTS (Claims to Windows Token Service)|[Declarações para C2WTS&#41; e Reporting Services &#40;do serviço de token do Windows](../../../2014/sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)|  
  
## <a name="migration-checklist"></a>Lista de verificação de migração  
 A seguir é apresentada uma lista das etapas básicas de uma migração de uma instalação existentes para uma nova instalação.  
  
|Etapa|Link|  
|----------|----------|  
|Instale e configure o novo servidor. Isso inclui o seguinte:<br /><br /> Ferramenta de preparação de produtos do SharePoint 2010<br /><br /> Produto do SharePoint 2010<br /><br /> SharePoint 2010 SP1<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint<br /><br /> Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint 2010|[Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Crie pelo menos um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Backup de bancos de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Backup de chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Restaurar o banco de dados e as chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Mapear todos os aplicativos Web para novos aplicativos de serviços do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|A nova instalação **está funcional agora**|  
|Remova a URL de integração no servidor antigo.|Na Administração Central do SharePoint, na página **Configurações de Aplicativo Gerais** , clique em **Integração do Reporting Services**.|  
|Desinstale o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da instalação antiga, se desejar.||  
  
## <a name="next-steps"></a>Próximas etapas  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services instalação &#40;do SharePoint 2010&#41;e SharePoint 2013](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [Diretrizes para usar SQL Server recursos de BI em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)   
 [Combinações com suporte do SharePoint e Reporting Services Server e suplemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
  
