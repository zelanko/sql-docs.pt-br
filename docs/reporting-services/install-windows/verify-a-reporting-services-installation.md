---
title: "Verifique se o Reporting Services instalação | Microsoft Docs"
ms.custom: 
ms.date: 06/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- Report Manager [Reporting Services], verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a5849b6240557cd1682d08210f256e0edabfa70b
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="verify-a-reporting-services-installation"></a>Verificar uma instalação do Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser instalados em um de dois modos: Nativo ou SharePoint. As etapas que você deve seguir para verificar a instalação dependem do modo do servidor de relatório.  
  
##  <a name="bkmk_sharepointmode"></a> Verificar a instalação do modo do SharePoint  
  
### <a name="to-verify-the-reporting-services-service"></a>Para verificar o serviço Reporting Services  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar serviços no servidor** no grupo **Configurações do Sistema** .  
  
2.  Verifique se o **Serviço SQL Server Reporting Services** está instalado e no estado **Executando** .  
  
     Se você não vir o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na lista, verifique se o serviço está instalado. Para obter mais informações, veja [Instalar o Primeiro Servidor de Relatório no Modo do SharePoint](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).  
  
### <a name="to-verify-the-service-application"></a>Para verificar o aplicativo de serviço  
  
1.  Para verificar na Administração Central que você tem pelo menos um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , clique em **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo** .  
  
2.  Verifique se há um aplicativo de serviço do tipo **Aplicativo de Serviço SQL Server Reporting Services** e um proxy de aplicativo correspondente.  
  
3.  Clique **próximo** ao nome do aplicativo de serviço e clique em **Propriedades** na barra de ferramentas do SharePoint.  Se você clicar no nome do aplicativo de serviço, serão abertas as páginas de Gerenciamento do aplicativo de serviço, não na página de propriedades.  
  
4.  Verifique se a **Associação de Aplicativo Web** está configurada para apontar para o aplicativo Web desejado.  
  
### <a name="to-verify-the-site-collection-feature"></a>Para verificar os Recursos da Coleção de Sites  
  
1.  Nas configurações do site, clique em **Recursos da Coleção de Sites** no grupo **Administração da Coleção de Sites** .  
  
2.  Verifique se o **Recurso de Integração do Servidor de Relatório** está ativo.  
  
### <a name="to-verify-reporting-server-content-types"></a>Para verificar tipos de conteúdo do servidor de relatório  
  
1.  Para verificar ou adicionar tipos de conteúdo do servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="to-verify-you-can-launch-report-builder"></a>Para verificar se você pode iniciar o Construtor de Relatórios  
  
1.  Na biblioteca de documentos, clique em **Documentos** na faixa de opções do SharePoint.  
  
2.  Clique em **Novo Documento** e clique em **Relatório do Construtor de Relatórios**. Se você não vir essa opção, examine o procedimento anterior sobre como adicionar os tipos de conteúdo do servidor de relatório a uma biblioteca.  
  
### <a name="create-a-basic-report"></a>Criar um relatório básico  
  
1.  Em uma biblioteca de documentos do SharePoint, crie um relatório básico do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que contém somente uma caixa de texto, por exemplo, um título. O relatório não contém fonte de dados ou conjunto de dados. A meta é verificar se você pode abrir o Construtor de Relatórios e um relatório básico será visualizado.  
  
2.  Salve o relatório em uma biblioteca de documentos e execute o relatório da biblioteca. Para obter mais informações sobre como criar relatórios com o Construtor de Relatórios, veja [Iniciar o Construtor de Relatórios](http://msdn.microsoft.com/en-us/8c8c7d2e-b315-418d-bf65-90e7685e4259).  
  
### <a name="reporting-services-samples"></a>Exemplos do Reporting Services  
  
1.  Concluir um dos tutoriais do Reporting Services. Para obter mais informações, consulte [tutoriais do Reporting Services &#40; SSRS &#41; ](../../reporting-services/reporting-services-tutorials-ssrs.md).  
  
2.  Baixe o banco de dados de exemplo do Adventure Works e os relatórios de exemplo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do CodePlex. Para obter mais informações, consulte os [Exemplos de relatórios do AdventureWorks](https://msftrsprodsamples.codeplex.com/wikipage?title=SS2012!AdventureWorks2012%20Report%20Samples&referringTitle=Home).  
  
##  <a name="bkmk_nativemode"></a> Verificar uma instalação no modo Nativo  
 Quando você instala um servidor de relatório do modo Nativo usando a configuração padrão, a Instalação instala e implanta o servidor. Você pode verificar se a Instalação implantou o servidor de relatório executando alguns testes simples. Você deve ser um administrador local para executar essas etapas. Para permitir que outros usuários executem o teste, você deve configurar o acesso ao servidor de relatório para tais usuários.  
  
### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>Para verificar se o servidor de relatório está instalado e em execução  
  
1.  Execute a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e se conecte à instância do servidor de relatório recém-instalada. A página URL do Serviço Web inclui um link para o serviço Web Servidor de Relatórios. Clique no link para verificar se você pode acessar o servidor. Se o banco de dados do servidor de relatório não estiver configurado, faça isso primeiro antes de clicar no link.  
  
2.  Abra os aplicativos do console Serviços e verifique se o serviço Servidor de Relatório está em execução. Para exibir o status do serviço Servidor de Relatório, clique em **Iniciar**, aponte para **Painel de Controle**, clique duas vezes em **Ferramentas Administrativas**e clique duas vezes em **Serviços**. Quando a lista de serviços for exibida, role até **Servidor de Relatório (MSSQLSERVER)**. O status deve ser **Iniciado**.  
  
3.  Abra um navegador e digite a URL do servidor de relatório na barra de endereço. O endereço consiste no nome do servidor e no nome do diretório virtual especificados para o servidor de relatório durante a instalação. Por padrão, o diretório virtual do servidor de relatório é denominado **ReportServer**. Você pode usar a URL a seguir para verificar a instalação do servidor de relatório: http://*\<nome do computador >*/ReportServer*\<_instance name >*. A URL será diferente se você tiver instalado o servidor de relatório como uma instância nomeada. Para obter mais informações sobre o formato de URL, consulte [Configurar URLs do servidor de relatório &#40; Gerenciador de configurações do SSRS &#41; ](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md). Se você for um administrador local no Windows Vista ou Windows Server 2008, consulte [configurar um servidor de relatório do modo nativo para administração Local &#40; SSRS &#41; ](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
4.  Execute relatórios para testar as operações do servidor de relatório. Para esta etapa, você pode criar um relatório de exemplo de um tutorial. Para obter mais informações, consulte [criar um relatório de tabela básico &#40; Tutorial do SSRS &#41; ](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
### <a name="to-verify-that-the-includessrswebportalincludesssrswebportalmd-is-installed-and-running"></a>Para verificar se o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] está instalado e em execução  
  
1.  Abra um navegador e digite a URL do Portal da Web na barra de endereço. O endereço consiste no nome do servidor e no nome do diretório virtual especificados para o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] durante a instalação ou na página URL do Portal da Web da ferramenta Configuração do Reporting Services. Por padrão, o diretório virtual do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] é **Relatórios**. Você pode usar a seguinte URL para verificar a instalação do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] :  
  
     http://*\<nome do computador >*/Reports*\<_instance name >*.  
  
2.  Use o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para criar uma nova pasta ou carregar um arquivo a fim de testar se as condições são devolvidas para o banco de dados do servidor de relatório. Se essas operações obtiverem êxito, a conexão estará funcional.  
  
     Para obter mais informações, consulte [Portal Web &#40; Modo nativo do SSRS &#41; ](http://msdn.microsoft.com/en-us/7349e626-6ed5-4d21-b05f-cf042ad9ad70).  
  
### <a name="to-verify-that-report-designer-is-installed-and-running"></a>Para verificar se o Designer de Relatórios está instalado e em execução  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e crie um novo projeto com base em um tipo de projeto do Servidor de Relatório. Para obter mais informações sobre como usar o Assistente de projeto do servidor de relatório, consulte [Reporting Services no SQL Server Data Tools &#40; SSDT &#41; ](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md) nos Manuais Online do SQL Server.  
  
2.  Se você tiver instalado exemplos de relatório, precisará abrir os arquivos de projeto do relatório de exemplo e publicar os relatórios em um servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar um problema da instalação do Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Causa e resolução de erros do Reporting Services](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  

