---
title: "Ativar e desativar recursos do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Reporting Services, configuração"
  - "segurança [Reporting Services], estratégias"
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 9
---
# Ativar e desativar recursos do Reporting Services
  Você pode desativar os recursos do servidor de relatório que não são usados como parte de uma estratégia de bloqueio para reduzir a superfície de ataque de um servidor de relatório de produção. Na maioria dos casos, você deve executar os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] simultaneamente para usar toda a funcionalidade disponível no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. No entanto, dependendo de seu modelo de implantação, você pode desabilitar os recursos dos quais não precisa. Por exemplo, você pode habilitar apenas o processamento em segundo plano se todo o processamento de relatórios for configurado como operações agendadas. Da mesma maneira, você pode executar somente o serviço Web Servidor de Relatório se quiser apenas relatórios interativos sob demanda.  
  
 Os procedimentos descritos neste tópico mostram como desativar recursos do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . É possível configurar recursos de maneiras diferentes; por exemplo, editando o arquivo `RsReportServer.config` diretamente ou usando a faceta **Configuração da Área de Superfície do Reporting Services** do Gerenciamento Baseado em Políticas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Use os links para localizar o(s) procedimento(s) que explica(m) como ativar ou desativar um recurso:  
  
-   [serviço Web Servidor de Relatórios](#RSWebSvc)  
  
-   [Eventos e processamento agendados](#Sched)  
  
-   [Gerenciador de Relatórios](#ReportManager)  
  
-   [Construtor de Relatórios](#ReportBuilder)  
  
-   [Segurança Integrada do Windows para fontes de dados de relatório](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> serviço Web Servidor de Relatórios  
  
#### Para ativar ou desativar o serviço Web Servidor de Relatórios editando a configuração  
  
1.  Abra o arquivo `RsReportServer.config` em um editor de texto. Para obter mais informações, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para ativar o serviço Web Servidor de Relatórios, defina **IsWebServiceEnabled** como **true**:  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  Para desativar o serviço Web Servidor de Relatórios, defina **IsWebServiceEnabled** como **false**:  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  Salve as alterações e feche o arquivo.  
  
#### Para ativar ou desativar o serviço Web Servidor de Relatórios usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nó [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], aponte para **Políticas** e clique em **Facetas**.  
  
3.  Na lista **Faceta** , selecione **Configuração da Área de Superfície do Reporting Services**.  
  
4.  Em **Propriedades da Faceta**:  
  
    -   Para ativar o serviço Web Servidor de Relatórios, defina **WebServiceAndHTTPAccessEnabled** como **True**.  
  
    -   Para desativar o serviço Web Servidor de Relatórios, defina **WebServiceAndHTTPAccessEnabled** como **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> Eventos e entrega agendados  
  
#### Para ativar ou desativar eventos e entrega agendados editando a configuração  
  
1.  Abra o arquivo RsReportServer.config em um editor de texto. Para obter mais informações, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para ativar o processamento e a entrega agendados de relatórios, defina **IsSchedulingService**, **IsNotificationService**e **IsEventService** como **true**:  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  Para desativar o processamento e a entrega agendados de relatórios, defina **IsSchedulingService**, **IsNotificationService**e **IsEventService** como **false**:  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  Salve as alterações e feche o arquivo.  
  
> [!NOTE]  
>  Não é possível desativar completamente o processamento em segundo plano porque ele fornece a funcionalidade de manutenção de banco de dados que é necessária para operações de servidor.  
  
#### Para ativar ou desativar eventos e entrega agendados usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nó [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], aponte para **Políticas** e clique em **Facetas**.  
  
3.  Na lista **Faceta** , selecione **Configuração da Área de Superfície do Reporting Services**.  
  
4.  Em **Propriedades da Faceta**:  
  
    -   Para ativar eventos e entrega agendados, defina **ScheduleEventsAndReportDeliveryEnabled** como **True**.  
  
    -   Para desativar eventos e entrega agendados, defina **ScheduleEventsAndReportDeliveryEnabled** como **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Não é possível desativar completamente o processamento em segundo plano porque ele fornece a funcionalidade de manutenção de banco de dados que é necessária para operações de servidor.  
  
##  <a name="ReportManager"></a> Gerenciador de Relatórios  
  
#### Para ativar ou desativar o Gerenciador de Relatórios editando a configuração  
  
1.  Abra o arquivo RsReportServer.config em um editor de texto. Para obter instruções, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para ativar o Gerenciador de Relatórios, defina **IsReportManagerEnabled** como **true**:  
  
    ```  
    <IsReportManagerEnabled>true</IsReportManagerEnabled>  
    ```  
  
3.  Para desativar o Gerenciador de Relatórios, defina **IsReportManagerEnabled** como **false**:  
  
    ```  
    <IsReportManagerEnabled>false</IsReportManagerEnabled>  
    ```  
  
4.  Salve as alterações e feche o arquivo.  
  
#### Para ativar ou desativar o Gerenciador de Relatórios usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No **Pesquisador de Objetos**, clique com o botão direito do mouse no nó [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], aponte para **Políticas** e clique em **Facetas**.  
  
3.  Na lista **Faceta** , selecione **Configuração da Área de Superfície do Reporting Services**.  
  
4.  Em **Propriedades da Faceta**:  
  
    -   Para ativar o Gerenciador de Relatórios, defina **ReportManagerEnabled** como **True**.  
  
    -   Para desativar o Gerenciador de Relatórios, defina **ReportManagerEnabled** como **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ReportBuilder"></a> Construtor de Relatórios  
  
#### Para ativar ou desativar o Construtor de Relatórios usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Servidor** , em **Selecionar uma página**, clique em **Segurança**.  
  
    -   Para ativar o Construtor de Relatórios, selecione a opção **Habilitar execuções de relatórios ad hoc** .  
  
    -   Para desativar o Construtor de Relatórios, desmarque a opção **Habilitar execuções de relatórios ad hoc** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Segurança integrada do Windows  
  
#### Para ativar ou desativar a segurança Integrada do Windows usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Servidor** , em **Selecionar uma página**, clique em **Segurança**.  
  
    -   Para ativar a segurança Integrada do Windows, selecione a opção **Habilitar a segurança Integrada do Windows para as fontes de dados do relatório** .  
  
    -   Para desativar a segurança Integrada do Windows, desmarque a opção **Habilitar a segurança Integrada do Windows para as fontes de dados do relatório** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Gerenciador de Configurações do Reporting Services (modo nativo do SSRS).](http://msdn.microsoft.com/pt-br/63519ef4-e68a-42fb-9cf7-31228ea4e434)  
  
  