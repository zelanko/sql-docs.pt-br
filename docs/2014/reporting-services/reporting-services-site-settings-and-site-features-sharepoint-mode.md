---
title: Configurações de Site e recursos de Site (modo SharePoint) do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 1128105b7334fc5bf81fd72b9e178c15634a1cab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005465"
---
# <a name="reporting-services-site-settings-and-site-featuressharepoint-mode"></a>Configurações de Site e Recursos de Site do Reporting Services (Modo SharePoint)
  O modo SharePoint do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] tem vários recursos personalizados em nível de site e um recurso de site que podem ser gerenciados na página Configurações de Site do SharePoint. As configurações abrangem todo o site e afetam todos os aplicativos de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Você deve ter permissões de Gerenciador de Conteúdo e de Administrador de Sistema para exibir essa página.  
  
|Configuração do site|Description|  
|------------------|-----------------|  
|Configuração de site do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Configurações de todo o site descritas neste tópico.|  
|Gerenciar Alertas de Dados|Gerenciamento do recurso Alerta de Dados.|  
|Sincronização de Arquivos do Servidor de Relatório|Um recurso em nível de site que é desativado por padrão.<br /><br /> Sincroniza arquivos do Servidor de Relatório (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) de uma biblioteca de documentos do SharePoint com o servidor de relatório quando os arquivos são adicionados ou atualizados diretamente na biblioteca de documentos.<br /><br /> Para obter mais informações, consulte [ativar o recurso de sincronização de arquivos de servidor de relatório na Administração Central do SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>Para abrir a página Configurações de Site do Reporting Services  
  
1.  No menu **Ações do Site** do site do SharePoint, clique em **Configurações de Site**.  
  
2.  Na seção **Reporting Services** , clique em **Configurações de Site do Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opções de Configurações de Site do Reporting Services  
  
|Opção|Description|  
|------------|-----------------|  
|**Habilitar download do controle ActiveX RSClientPrint**|O controle exibe uma caixa de diálogo de impressão personalizada que fornece recursos de suporte comuns a outras caixas de diálogo de impressão, inclusive visualização de impressão, seleções de páginas para definir páginas e intervalos específicos, margens de páginas e orientação de página. Para saber mais sobre o controle, consulte [Usando o controle RSClientPrint em aplicativos personalizados](report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Habilitar erros remotos em modo local**|Mostrar ou ocultar mensagens de erro detalhadas em computadores remotos ao executar em modo local. Se você ver uma mensagem de erro semelhante à seguinte, pode ser útil habilitar erros remotos:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Habilitar metadados de acessibilidade para relatórios**|Ativar metadados de acessibilidade na saída HTML para relatórios|  
|**Habilitar Dimensionamento de Visualização de Dados para Ajuste Exato em Relatórios**|Configurar o comportamento de ajuste de visualização de dados dentro de um tablix, para corrigir exatamente. Isso inclui gráfico, medidor e mapa. Quando desabilitado, o comportamento é de ajuste aproximado de visualizações de dados, o que pode deixar algum espaço em branco. Esta configuração se aplica somente à renderização na Web Part do visualizador de relatórios. Para gerenciar esse comportamento para a renderização do lado do servidor, é necessário modificar o arquivo **rsreportserver.config** . Para obter mais informações, consulte o seguinte:<br /><br /> [Arquivo de configuração RSReportServer](report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Personalizar a renderização de parâmetros de extensão em rsreportserver. config](customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [Configurações de informações do dispositivo HTML](html-device-information-settings.md).<br /><br /> Quando Exato é habilitado, o desempenho pode ser afetado porque o processamento para determinar o tamanho exato pode levar mais tempo que no ajuste aproximado.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
  