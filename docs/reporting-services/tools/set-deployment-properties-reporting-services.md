---
title: "Definir propriedades de implantação (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], deploying
- publishing reports [Reporting Services]
- properties [Reporting Services], deployment
- deploying reports [Reporting Services]
ms.assetid: 18201ca0-bf4a-484f-b3a2-95d1046a6a9b
caps.latest.revision: "44"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 555497ecba823a6c13babbbfd1958bf293bd1f9b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="set-deployment-properties-reporting-services"></a>Definir propriedades de implantação (Reporting Services)
  No[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você deve especificar o servidor de relatório e opcionalmente as pastas para os relatórios e fontes de dados compartilhados, de forma a poder publicar os itens no projeto do Servidor de Relatório para um servidor de relatório. As propriedades e os valores que o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] precisa para compilar, visualizar e implantar relatórios são armazenados em configurações de projeto do Servidor de Relatório. Você pode criar vários conjuntos nomeados para essas propriedades de projetos, para que você possa alternar de maneira conveniente entre os conjuntos de propriedades. Cada conjunto de propriedades é uma configuração. Por exemplo, você pode ter uma configuração para publicar relatórios em um servidor de teste e uma configuração diferente para publicar relatórios para um servidor de produção.  
  
 Use o Gerenciador de Configuração para criar e gerenciar conjuntos de propriedades de projeto em configurações de projeto. O Gerenciador de Configurações é um recurso suportado pelo [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], no qual o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] se baseia.  
  
> [!NOTE]  
>  Não confunda esse recurso com o Gerenciador de Configuração do Reporting Services, usado para configurar os Reporting Services depois da instalação. Para obter mais informações, consulte [Configurar e administrar um servidor de relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md).  
  
> [!NOTE]  
>  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], a ação de publicar relatórios de um projeto ou solução do Servidor de Relatório é conhecida como *implantar relatórios*.  
  
### <a name="to-set-deployment-properties"></a>Para definir as propriedades de implantação  
  
1.  Clique com o botão direito do mouse no projeto de relatório e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Páginas de Propriedades** do projeto, selecione uma configuração a ser editada da lista **Configuração** . As configurações comuns são **DebugLocal**, **Debug**e **Release**.  
  
    > [!NOTE]  
    >  Você pode usar várias configurações para alternar rapidamente entre diferentes servidores de relatório ou configurações.  
  
3.  Na caixa de texto **OutputPath**  , digite ou cole o caminho no sistema de arquivos local para armazenar a definição de relatório usada na verificação de build, implantação e visualização de relatórios. O caminho deve ser diferente do caminho que você usa para o projeto e um caminho relativo que é uma pasta filho sob o caminho do projeto.  
  
4.  Na caixa de texto **ErrorLevel**  , digite a severidade dos problemas de compilação que são relatados como erros. Problemas que ocorrem ao compilar relatórios, fontes de dados ou outros recursos de projeto com níveis de severidade menor ou igual ao valor de **ErrorLevel**  são relatados como erros; caso contrário, os problemas são relatados como avisos. Qualquer erro causará falha na tarefa de compilação. Os níveis de severidade válidos são de 0 a 4, inclusive. O valor padrão é 2.  
  
     **ErrorLevel** pode ser usado para aumentar ou diminuir a sensibilidade da compilação. Por exemplo, quando um relatório com um mapa é compilado durante a implantação em um servidor de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , um erro é exibido por padrão e ocorre falha na compilação do relatório. Se você abaixar o **ErrorLevel** , o mapa será removido do relatório, um aviso será exibido e a compilação do relatório continuará.  
  
5.  Na lista **StartItem**  , selecione um relatório a ser exibido na janela de visualização ou em uma janela do navegador quando o projeto de relatório for executado.  
  
6.  Na lista **OverwriteDataSources** , selecione **True** para substituir a fonte de dados compartilhados no servidor cada vez que elas forem publicadas, ou selecione **False** para manter a fonte de dados no servidor.  
  
7.  Na lista **TargetServerVersion** , selecione a versão do SQL Server 2016 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou selecione **Detectar Versão** para determinar automaticamente a versão instalada no servidor identificado pela propriedade **URL do TargetServer** . O valor padrão é **SQL Server 2016 ou posterior**.  
  
     Use **TargetServerVersion** para personalizar os relatórios criados, colocados no caminho especificado em OutputPath, para a versão do servidor de relatório especificada em **TargetServer URL**.  
  
8.  Na caixa de texto **TargetDataSourceFolder** , digite a pasta no servidor de relatórios no qual as fontes de dados compartilhadas publicadas devem ser posicionadas. O valor padrão para **TargetDataSourceFolder** é Fontes de Dados. Se você deixar este valor em branco, as fontes de dados serão publicadas no local especificado em **TargetReportFolder**.  
  
9. Na caixa de texto **TargetReportFolder** , digite a pasta no servidor de relatórios no qual os relatórios publicados devem ser posicionados. O valor padrão para **TargetReportFolder**  é o nome do projeto de relatório.  
  
    > [!NOTE]  
    >  Para um servidor de relatórios executado no modo nativo, você deverá ter permissões de **Publicação** na pasta de destino para publicar relatórios nessa pasta. As permissões de publicação são fornecidas por meio de uma atribuição de função que mapeia sua conta de usuário para uma função que inclui operações de publicação. Para obter mais informações, consulte [Criar e gerenciar atribuições](../../reporting-services/security/create-and-manage-role-assignments.md). Para um servidor de relatórios executado no modo integrado do SharePoint, você deve ter permissão de **Membro** ou **Proprietário** no site do SharePoint. Para obter mais informações, consulte [Referência à permissão de listas e sites do SharePoint para itens do Servidor de Relatório](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
10. Na caixa de texto **TargetServerURL** , digite a URL do servidor de relatórios de destino. Antes de publicar um relatório, defina essa propriedade com uma URL de servidor de relatório válida. Ao publicar em um servidor de relatório executado no modo nativo, use a URL do diretório virtual do servidor de relatório (por exemplo, http:*//server/reportserver* ou https:*//server/reportserver)*. Este é o diretório virtual do servidor de relatório e não o Gerenciador de Relatórios.  
  
     Quando publicar em um servidor de relatório executado no modo integrado do SharePoint, use uma URL de um site de nível superior ou subsite do SharePoint. Se você não especificar um site, o site de nível superior padrão será usado (por exemplo, http://*servername*, http://*servername*/*site* ou http://*servername*/*site*/*subsite*).  
  
### <a name="to-set-configuration-manager-properties"></a>Para definir as propriedades do Gerenciador de Configuração  
  
1.  Clique com o botão direito do mouse no projeto de relatório e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Páginas de Propriedades** do projeto, clique no **Gerenciador de Configuração**.  
  
3.  Na caixa de diálogo **Gerenciador de Configuração** , selecione a configuração a ser editado. A configuração ativa no momento é exibida como **Ativa(***\<configuration>***)**.  
  
4.  Em **Contextos do Projeto**, para cada projeto na solução, selecione ou desmarque **Build** ou **Deploy**.  
  
    > [!NOTE]  
    >  Se **Build** estiver selecionado, o Designer de Relatórios cria o projeto de relatórios e procura erros antes de exibir ou publicar em um servidor de relatórios. Se **Deploy** estiver selecionado, o Designer de Relatórios publicará os relatórios no servidor de relatórios conforme definido nas propriedades de implantação. Se **Deploy** não estiver selecionado, o Designer de Relatórios exibirá o relatório especificado na propriedade **StartItem** em uma janela de visualização local.  
  
## <a name="see-also"></a>Consulte também  
 [Publicando fontes de dados e relatórios](../../reporting-services/reports/publishing-data-sources-and-reports.md)   
 [Visualizar relatórios](../../reporting-services/reports/previewing-reports.md)   
 [Ajuda F1 do Designer de Relatórios](../../reporting-services/tools/report-designer-f1-help.md)   
 [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Caixa de diálogo Páginas de Propriedades do Projeto](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Publicar relatórios em um servidor de relatórios](../../reporting-services/reports/publishing-reports-to-a-report-server.md)  
  
  
