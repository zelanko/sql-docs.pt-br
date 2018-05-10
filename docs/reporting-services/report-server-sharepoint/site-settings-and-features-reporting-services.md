---
title: Configurações de site e recursos de site do Reporting Services (modo do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d376ca984ee2666c8f84a46d3a7895c911d0c719
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="reporting-services-site-settings-and-site-features-sharepoint-mode"></a>Configurações de site e recursos de site do Reporting Services (modo do SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

O modo do SharePoint do Reporting Services contém vários recursos personalizados em nível de site e um recurso de site que podem ser gerenciados na página Configurações de Site do SharePoint. As configurações abrangem todo o site e afetam todos os aplicativos de serviço do Reporting Services. Você deve ter permissões de Gerenciador de Conteúdo e de Administrador de Sistema para exibir essa página.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

|Configuração do site|Description|  
|------------------|-----------------|  
|Configurações de Site do Reporting Services|Configurações que abrangem todo o site descritas neste tópico.|  
|Gerenciar Alertas de Dados|Gerenciamento do recurso Alerta de Dados.|  
|Sincronização de Arquivos do Servidor de Relatório|Um recurso em nível de site que é desativado por padrão.<br /><br /> Sincroniza arquivos do Servidor de Relatório (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) de uma biblioteca de documentos do SharePoint com o servidor de relatório quando os arquivos são adicionados ou atualizados diretamente na biblioteca de documentos.<br /><br /> Para obter mais informações, consulte [Ativar o recurso de sincronização de arquivo do Servidor de Relatório na Administração Central do SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)|  
  
## <a name="open-the-reporting-services-site-settings-page"></a>Abrir a página de configurações de site do Reporting Services
  
1.  No menu **Ações do Site** do site do SharePoint, selecione **Configurações de Site**.  
  
2.  Na seção **Reporting Services**, selecione **Configurações de Site do Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opções de configurações de site do Reporting Services
  
|Opção|Description|  
|------------|-----------------|  
|**Habilitar download do controle ActiveX RSClientPrint**|O controle exibe uma caixa de diálogo de impressão personalizada que fornece recursos de suporte comuns a outras caixas de diálogo de impressão, inclusive visualização de impressão, seleções de páginas para definir páginas e intervalos específicos, margens de páginas e orientação de página. Para saber mais sobre o controle, consulte [Usando o controle RSClientPrint em aplicativos personalizados](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Habilitar erros remotos em modo local**|Mostrar ou ocultar mensagens de erro detalhadas em computadores remotos ao executar em modo local. Se você ver uma mensagem de erro semelhante à seguinte, pode ser útil habilitar erros remotos:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Habilitar metadados de acessibilidade para relatórios**|Ativar metadados de acessibilidade na saída HTML para relatórios|  
|**Habilitar Dimensionamento de Visualização de Dados para Ajuste Exato em Relatórios**|Configurar o comportamento de ajuste de visualização de dados dentro de um tablix, para corrigir exatamente. Isso inclui gráfico, medidor e mapa. Quando desabilitado, o comportamento é de ajuste aproximado de visualizações de dados, o que pode deixar algum espaço em branco. Essa configuração se aplica somente à renderização na web part do Visualizador de Relatórios. Para gerenciar esse comportamento para a renderização do lado do servidor, é necessário modificar o arquivo **rsreportserver.config**. Para obter mais informações, consulte o seguinte:<br /><br /> [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Personalizar parâmetros de extensão de renderização em RSReportServer.config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [Configurações de informações do dispositivo HTML](../../reporting-services/html-device-information-settings.md).<br /><br /> Quando Exato é habilitado, o desempenho pode ser afetado porque o processamento para determinar o tamanho exato pode levar mais tempo que no ajuste aproximado.|  
  
## <a name="see-also"></a>Confira também

 [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
