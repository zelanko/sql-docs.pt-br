---
title: Ativar ou desativar recursos do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- security [Reporting Services], strategies
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 75845ddac250c70078c8ee43d885b7d2b99a69a1
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031087"
---
# <a name="turn-reporting-services-features-on-or-off"></a>Ativar e desativar recursos do Reporting Services
  Você pode desativar os recursos do servidor de relatório que não são usados como parte de uma estratégia de bloqueio para reduzir a superfície de ataque de um servidor de relatório de produção. Na maioria dos casos, você deve executar os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] simultaneamente para usar toda a funcionalidade disponível no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. No entanto, dependendo de seu modelo de implantação, você pode desabilitar os recursos dos quais não precisa. Por exemplo, você pode habilitar apenas o processamento em segundo plano se todo o processamento de relatórios for configurado como operações agendadas. Da mesma maneira, você pode executar somente o serviço Web Servidor de Relatório se quiser apenas relatórios interativos sob demanda.  
  
 Os procedimentos descritos neste tópico mostram como desativar recursos do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . É possível configurar recursos de maneiras diferentes; por exemplo, editando o arquivo `RsReportServer.config` diretamente ou usando a faceta **Configuração da Área de Superfície do Reporting Services** do Gerenciamento Baseado em Políticas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Use os links para localizar o(s) procedimento(s) que explica(m) como ativar ou desativar um recurso:  
  
-   [serviço Web Servidor de Relatórios](#RSWebSvc)  
  
-   [Eventos e processamento agendados](#Sched)  
  
-   [Gerenciador de Relatórios](#ReportManager)  
  
-   [Construtor de Relatórios](#ReportBuilder)  
  
-   [Segurança Integrada do Windows para fontes de dados de relatório](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> Report Server Web Service  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-editing-configuration"></a>Para ativar ou desativar o serviço Web Servidor de Relatórios editando a configuração  
  
1.  Abra o arquivo `RsReportServer.config` em um editor de texto. Para obter mais informações, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para ativar o serviço Web Servidor de Relatórios, defina `IsWebServiceEnabled` como `true`:  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  Para desativar o serviço Web Servidor de Relatórios, defina `IsWebServiceEnabled` como `false`:  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  Salve as alterações e feche o arquivo.  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-using-sql-server-management-studio"></a>Para ativar ou desativar o serviço Web Servidor de Relatórios usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nó [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , aponte para **Políticas**e clique em **Facetas**.  
  
3.  Na lista **Faceta** , selecione **Configuração da Área de Superfície do Reporting Services**.  
  
4.  Em **Propriedades da Faceta**:  
  
    -   Para ativar o serviço Web servidor de relatório, defina **WebServiceAndHTTPAccessEnabled** para `True`.  
  
    -   Para desativar o serviço Web servidor de relatório, defina **WebServiceAndHTTPAccessEnabled** para `False`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> Eventos e entrega agendados  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-editing-configuration"></a>Para ativar ou desativar eventos e entrega agendados editando a configuração  
  
1.  Abra o arquivo RsReportServer.config em um editor de texto. Para obter mais informações, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para ativar o processamento e a entrega agendados de relatórios, defina `IsSchedulingService`, `IsNotificationService` e `IsEventService` como `true`:  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  Para desativar o processamento e a entrega agendados de relatórios, defina `IsSchedulingService`, `IsNotificationService` e `IsEventService` como `false`:  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  Salve as alterações e feche o arquivo.  
  
> [!NOTE]  
>  Não é possível desativar completamente o processamento em segundo plano porque ele fornece a funcionalidade de manutenção de banco de dados que é necessária para operações de servidor.  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-using-sql-server-management-studio"></a>Para ativar ou desativar eventos e entrega agendados usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nó [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , aponte para **Políticas**e clique em **Facetas**.  
  
3.  Na lista **Faceta** , selecione **Configuração da Área de Superfície do Reporting Services**.  
  
4.  Em **Propriedades da Faceta**:  
  
    -   Para ativar eventos e entrega agendados, defina **ScheduleEventsAndReportDeliveryEnabled** para `True`.  
  
    -   Para desativar eventos e entrega agendados, defina **ScheduleEventsAndReportDeliveryEnabled** para `False`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Não é possível desativar completamente o processamento em segundo plano porque ele fornece a funcionalidade de manutenção de banco de dados que é necessária para operações de servidor.  
  
##  <a name="ReportManager"></a> Gerenciador de relatórios  
  
#### <a name="to-turn-on-or-off-report-manager-by-editing-configuration"></a>Para ativar ou desativar o Gerenciador de Relatórios editando a configuração  
  
1.  Abra o arquivo RsReportServer.config em um editor de texto. Para obter instruções, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para ativar o Gerenciador de Relatórios, defina `IsReportManagerEnabled` como `true`:  
  
    ```  
    <IsReportManagerEnabled>true</IsReportManagerEnabled>  
    ```  
  
3.  Para desativar o Gerenciador de Relatórios, defina `IsReportManagerEnabled` como `false`:  
  
    ```  
    <IsReportManagerEnabled>false</IsReportManagerEnabled>  
    ```  
  
4.  Salve as alterações e feche o arquivo.  
  
#### <a name="to-turn-on-or-off-report-manager-by-using-sql-server-management-studio"></a>Para ativar ou desativar o Gerenciador de Relatórios usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No **Pesquisador de Objetos**, clique com o botão direito do mouse no nó [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , aponte para **Políticas**e clique em **Facetas**.  
  
3.  Na lista **Faceta** , selecione **Configuração da Área de Superfície do Reporting Services**.  
  
4.  Em **Propriedades da Faceta**:  
  
    -   Para desativar o Gerenciador de relatórios, defina **ReportManagerEnabled** para `True`.  
  
    -   Para desativar o Gerenciador de relatórios, defina **ReportManagerEnabled** para `False`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ReportBuilder"></a> Construtor de Relatórios  
  
#### <a name="to-turn-on-or-off-report-builder-by-using-sql-server-management-studio"></a>Para ativar ou desativar o Construtor de Relatórios usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Servidor** , em **Selecionar uma página**, clique em **Segurança**.  
  
    -   Para ativar o Construtor de Relatórios, selecione a opção **Habilitar execuções de relatórios ad hoc** .  
  
    -   Para desativar o Construtor de Relatórios, desmarque a opção **Habilitar execuções de relatórios ad hoc** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Segurança integrada do Windows  
  
#### <a name="to-turn-on-or-off-windows-integrated-security-by-using-sql-server-management-studio"></a>Para ativar ou desativar a segurança Integrada do Windows usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você deseja configurar.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Servidor** , em **Selecionar uma página**, clique em **Segurança**.  
  
    -   Para ativar a segurança Integrada do Windows, selecione a opção **Habilitar a segurança Integrada do Windows para as fontes de dados do relatório** .  
  
    -   Para desativar a segurança Integrada do Windows, desmarque a opção **Habilitar a segurança Integrada do Windows para as fontes de dados do relatório** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
