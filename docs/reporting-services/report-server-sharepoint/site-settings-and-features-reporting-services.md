---
title: "Configurações de Site e recursos de Site (modo SharePoint) do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 044346bd4532c691861689662edbcbb37812b7ff
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="site-settings-and-features---reporting-services"></a>Configurações de site e recursos - Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O modo SharePoint tem vários recursos personalizados em nível de site e um recurso de site que podem ser gerenciados na página Configurações de Site do SharePoint. As configurações abrangem todo o site e afetam todos os aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você deve ter permissões de Gerenciador de Conteúdo e de Administrador de Sistema para exibir essa página.  
  
|Configuração do site|Description|  
|------------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuração de site|Configurações de todo o site descritas neste tópico.|  
|Gerenciar Alertas de Dados|Gerenciamento do recurso Alerta de Dados.|  
|Sincronização de Arquivos do Servidor de Relatório|Um recurso em nível de site que é desativado por padrão.<br /><br /> Sincroniza arquivos do Servidor de Relatório (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) de uma biblioteca de documentos do SharePoint com o servidor de relatório quando os arquivos são adicionados ou atualizados diretamente na biblioteca de documentos.<br /><br /> Para obter mais informações, consulte [Ativar o recurso de sincronização de arquivo do Servidor de Relatório na Administração Central do SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>Para abrir a página Configurações de Site do Reporting Services  
  
1.  No menu **Ações do Site** do site do SharePoint, clique em **Configurações de Site**.  
  
2.  Na seção **Reporting Services** , clique em **Configurações de Site do Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opções de Configurações de Site do Reporting Services  
  
|Opção|Description|  
|------------|-----------------|  
|**Habilitar download do controle ActiveX RSClientPrint**|O controle exibe uma caixa de diálogo de impressão personalizada que fornece recursos de suporte comuns a outras caixas de diálogo de impressão, inclusive visualização de impressão, seleções de páginas para definir páginas e intervalos específicos, margens de páginas e orientação de página. Para saber mais sobre o controle, consulte [Usando o controle RSClientPrint em aplicativos personalizados](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Habilitar erros remotos em modo local**|Mostrar ou ocultar mensagens de erro detalhadas em computadores remotos ao executar em modo local. Se você ver uma mensagem de erro semelhante à seguinte, pode ser útil habilitar erros remotos:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Habilitar metadados de acessibilidade para relatórios**|Ativar metadados de acessibilidade na saída HTML para relatórios|  
|**Habilitar Dimensionamento de Visualização de Dados para Ajuste Exato em Relatórios**|Configurar o comportamento de ajuste de visualização de dados dentro de um tablix, para corrigir exatamente. Isso inclui gráfico, medidor e mapa. Quando desabilitado, o comportamento é de ajuste aproximado de visualizações de dados, o que pode deixar algum espaço em branco. Esta configuração se aplica somente à renderização na Web Part do visualizador de relatórios. Para gerenciar esse comportamento para a renderização do lado do servidor, é necessário modificar o arquivo **rsreportserver.config** . Para obter mais informações, consulte o seguinte:<br /><br /> [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Personalizar parâmetros de extensão de renderização em RSReportServer.config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [Configurações de informações do dispositivo HTML](../../reporting-services/html-device-information-settings.md).<br /><br /> Quando Exato é habilitado, o desempenho pode ser afetado porque o processamento para determinar o tamanho exato pode levar mais tempo que no ajuste aproximado.|  
  
## <a name="see-also"></a>Consulte também  
 [Manage a Reporting Services SharePoint Service Application](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
