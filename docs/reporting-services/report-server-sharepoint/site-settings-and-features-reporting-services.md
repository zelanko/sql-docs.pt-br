---
title: "Configurações do site Reporting Services e o site de recursos (modo SharePoint) | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: ea81c248f302e322d981b90147d42cb83a4804cc
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="reporting-services-site-settings-and-site-features-sharepoint-mode"></a>Relatórios de configurações de site de serviços e recursos de site (modo SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Modo do Reporting Services SharePoint tem vários recursos personalizados nível do site e o recurso de site que pode ser gerenciado da página de configurações do Site do SharePoint. As configurações abrangem todo o site e afetam todos os aplicativos de serviço do Reporting Services. Você deve ter permissões de Gerenciador de Conteúdo e de Administrador de Sistema para exibir essa página.  

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

|Configuração do site|Description|  
|------------------|-----------------|  
|Configurações de Site do Reporting Services|Configurações de todo o site descritas neste tópico.|  
|Gerenciar Alertas de Dados|Gerenciamento do recurso Alerta de Dados.|  
|Sincronização de Arquivos do Servidor de Relatório|Um recurso em nível de site que é desativado por padrão.<br /><br /> Sincroniza arquivos do Servidor de Relatório (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) de uma biblioteca de documentos do SharePoint com o servidor de relatório quando os arquivos são adicionados ou atualizados diretamente na biblioteca de documentos.<br /><br /> Para obter mais informações, consulte [Ativar o recurso de sincronização de arquivo do Servidor de Relatório na Administração Central do SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)|  
  
## <a name="open-the-reporting-services-site-settings-page"></a>Abra a página de configurações de site do Reporting Services
  
1.  No site do SharePoint **ações do Site** menu, selecione **configurações do Site**.  
  
2.  No **Reporting Services** seção, selecione **configurações do Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opções de configuração de site do Reporting Services
  
|Opção|Description|  
|------------|-----------------|  
|**Habilitar download do controle ActiveX RSClientPrint**|O controle exibe uma caixa de diálogo de impressão personalizada que fornece recursos de suporte comuns a outras caixas de diálogo de impressão, inclusive visualização de impressão, seleções de páginas para definir páginas e intervalos específicos, margens de páginas e orientação de página. Para saber mais sobre o controle, consulte [Usando o controle RSClientPrint em aplicativos personalizados](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Habilitar erros remotos em modo local**|Mostrar ou ocultar mensagens de erro detalhadas em computadores remotos ao executar em modo local. Se você ver uma mensagem de erro semelhante à seguinte, pode ser útil habilitar erros remotos:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Habilitar metadados de acessibilidade para relatórios**|Ativar metadados de acessibilidade na saída HTML para relatórios|  
|**Habilitar Dimensionamento de Visualização de Dados para Ajuste Exato em Relatórios**|Configurar o comportamento de ajuste de visualização de dados dentro de um tablix, para corrigir exatamente. Isso inclui gráfico, medidor e mapa. Quando desabilitado, o comportamento é de ajuste aproximado de visualizações de dados, o que pode deixar algum espaço em branco. Essa configuração se aplica somente à renderização na web part do Visualizador de relatórios. Para gerenciar esse comportamento de renderização do lado do servidor, você precisa modificar o **rsreportserver. config** arquivo. Para obter mais informações, consulte o seguinte:<br /><br /> [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Personalizar parâmetros de extensão de renderização em RSReportServer.config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [Configurações de informações do dispositivo HTML](../../reporting-services/html-device-information-settings.md).<br /><br /> Quando Exato é habilitado, o desempenho pode ser afetado porque o processamento para determinar o tamanho exato pode levar mais tempo que no ajuste aproximado.|  
  
## <a name="see-also"></a>Consulte também

 [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  

