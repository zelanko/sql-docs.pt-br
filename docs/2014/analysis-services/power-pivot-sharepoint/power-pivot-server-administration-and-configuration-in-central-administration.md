---
title: Administração e configuração do servidor PowerPivot na administração central | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0bea6bb558e6ccafefbbb068fa3799eddff748a5
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547802"
---
# <a name="powerpivot-server-administration-and-configuration-in-central-administration"></a>Administração e configuração de servidor do PowerPivot na Administração Central
  A administração de servidor e a configuração do PowerPivot são realizadas por administradores de aplicativo de serviço do SharePoint, usando a Administração Central do SharePoint.  
  
 O PowerPivot para SharePoint deve ser configurado antes de ser usado. Após instalar o PowerPivot para SharePoint usando a Instalação do SQL Server, você poderá configurá-lo usando uma das seguintes abordagens:  
  
-   Ferramenta de Configuração do PowerPivot ou Ferramenta de Configuração do PowerPivot para SharePoint 2013  
  
-   Administração Central do SharePoint  
  
-   Cmdlets do PowerShell  
  
 Todas as três abordagens entregam um servidor completamente configurado.  
  
 Esta seção inclui tarefas para configurar o software usando a Administração Central. Execute pelo menos as três tarefas da configuração exigidas anotadas na lista abaixo.  
  
> [!IMPORTANT]  
>  Para o SharePoint 2010, o SharePoint 2010 Service Pack 1 (SP1) deve ser instalado antes da configuração do PowerPivot para SharePoint ou de um farm do SharePoint que usa um servidor de banco de dados do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Se você ainda não instalou o service pack; faça isso agora, antes de começar a configurar o servidor.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-central-administration"></a>Benefícios de configurar o PowerPivot para SharePoint usando a Administração Central  
 A Administração Central do SharePoint é o aplicativo administrativo de um farm do SharePoint. Se você for administrador de farm, pode preferir usar uma ferramenta familiar ao adicionar uma instância do PowerPivot para SharePoint a seu farm.  
  
 Em contraste com as Ferramentas de Configuração do PowerPivot ou cmdlets PowerShell, a Administração Central fornece páginas que especificam completamente todas as opções que você pode definir ao configurar um aplicativo ou servidor. Outras abordagens condensam o fluxo de trabalho de configuração em um número menor de etapas ou exigem conhecimento prévio de como configurar um servidor do SharePoint usando PowerShell.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Configuração do PowerPivot usando o Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot Configuration Tools](power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Link|Tipo|Descrição da tarefa|  
|----------|----------|----------------------|  
|[Implantar soluções PowerPivot para SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)|Obrigatório|Esta etapa instala os arquivos da solução que adicionam arquivos de programa e páginas de aplicativo ao farm e às coleções de sites.|  
|[Criar e configurar um aplicativo de serviço PowerPivot na Administração Central](create-and-configure-power-pivot-service-application-in-ca.md)|Obrigatório|Essa etapa provisiona o Serviço de Sistema PowerPivot.|  
|[Ativar a integração de recursos do PowerPivot para coleções de sites na Administração Central](activate-power-pivot-integration-for-site-collections-in-ca.md)|Obrigatório|Esta etapa ativa os recursos do PowerPivot no nível de coleção de sites.|  
|[Adicionar MSOLAP.5 como um provedor de dados confiável em Serviços do Excel](add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|Obrigatório|Esta etapa adiciona o provedor OLE DB do Analysis Services como um provedor de confiança em Serviços do Excel.|  
|[Atualização de dados PowerPivot com SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)|Recomendadas|A atualização de dados é opcional, porém recomendada. Ela permite programar atualizações autônomas ao dados PowerPivot em pastas de trabalho do Excel publicadas.|  
|[Configurar a conta de atualização de dados autônoma do PowerPivot &#40;PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)|Recomendadas|Esta etapa provisiona uma conta com finalidade especial que pode ser usada para executar trabalhos de atualização de dados no servidor.|  
|[Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|Opcional|A coleta de dados de uso é configurada por padrão. Você pode usar essas etapas para modificar as configurações padrão.|  
|[Configurar a atualização de dados dedicada ou o processamento somente de consulta &#40;PowerPivot para SharePoint&#41;](../configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)|Opcional|Uma instância do PowerPivot pode ser dedicada somente para trabalhos de atualização de dados ou consultas. Além disso, você pode modificar as configurações padrão para trabalhos de atualização de dados paralelos.|  
|[Configurar contas de serviço PowerPivot](configure-power-pivot-service-accounts.md)|Opcional|Explica como atualizar senhas ou alterar contas de serviço.|  
|[Conectar um aplicativo de serviço PowerPivot a um aplicativo Web do SharePoint na Administração Central](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|Opcional|Explica como modificar associações de serviço.|  
|[Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|Opcional|Explica como adicionar a Galeria PowerPivot como um local confiável.|  
|[Configurar e exibir arquivos de log do SharePoint e log de diagnóstico &#40;PowerPivot para SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)|Opcional|O log de eventos está configurado por padrão. Você pode usar essas etapas para modificar as configurações padrão.|  
|[Regras de integridade do PowerPivot - Configurar](configure-power-pivot-health-rules.md)|Opcional|As regras de integridade do servidor são configuradas por padrão. Você pode usar essas etapas para modificar algumas das configurações padrão.|  
|[Criar e personalizar uma galeria do PowerPivot](create-and-customize-power-pivot-gallery.md)|Opcional|Para instalações que você está configurando manualmente, este procedimento explica como criar uma biblioteca da Galeria PowerPivot que mostra miniaturas de imagem das pastas de trabalho PowerPivot que ela contém.|  
|[Adicione um tipo de conteúdo de conexão de modelo semântico de BI a uma biblioteca &#40;PowerPivot para SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)|Opcional|Explica como estender uma biblioteca de documentos para dar suporte à criação de arquivos de conexão de modelo semântico de BI.|  
  
## <a name="see-also"></a>Consulte Também  
 [Instalação do PowerPivot para SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Referência de definição de configuração &#40;PowerPivot para SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Recuperação de desastres para PowerPivot para SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
