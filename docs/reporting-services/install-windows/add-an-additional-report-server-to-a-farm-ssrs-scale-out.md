---
title: Adicionar um servidor de relatório a um farm (expansão do SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 17cffe2f1eaf94174301212c6bb926528c56c7d3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63225687"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>Adicionar um servidor de relatório a um farm (expansão SSRS)

  Adicionar um segundo ou mais servidores de relatório de modo do SharePoint ao seu farm do SharePoint pode melhorar o desempenho e o tempo de resposta do processamento do servidor de relatório. Se você perceber que o desempenho está mais lento à medida que você adiciona mais usuários, relatórios e outros aplicativos ao servidor de relatório, então a adição de servidores de relatório pode melhorar o desempenho. Isto também é recomendado para adicionar um segundo servidor de relatório para aumentar a disponibilidade de servidores de relatório quando houver problemas com hardware ou você estiver realizando manutenção geral em servidores individuais em seu ambiente. A partir da versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , as etapas para expansão de um ambiente do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo do SharePoint seguem a implantação padrão de farm do SharePoint e aproveita os recursos de balanceamento de carga do SharePoint.  
  
> [!IMPORTANT]  
>  Não há suporte expansão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, confira a seção [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de [Recursos compatíveis com as edições do SQL Server](~/sql-server/editions-and-components-of-sql-server-2017.md#SSRS).  
  
> [!TIP]  
>  A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , você não usa o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager para adicionar servidores e expandir servidores de relatório. Os produtos do SharePoint gerenciam a expansão dos serviços de relatório à medida que os servidores do SharePoint com o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são adicionados ao farm.  
  
 Para obter informações sobre como expandir os servidores de relatório do modo nativo, veja [Configurar uma implantação em expansão do servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
##  <a name="bkmk_loadbalancing"></a> Balanceamento de carga  
 O balanceamento de carga de aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será gerenciado automaticamente pelo SharePoint a menos que seu ambiente tenha uma solução de balanceamento de carga personalizada ou de terceiros. O comportamento padrão de balanceamento de carga do SharePoint é que cada Aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será balanceado em todos os servidores de aplicativos onde você iniciou o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para verificar se o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado e iniciado, clique em **Gerenciar serviços no servidor** na Administração Central do SharePoint.  
  
##  <a name="bkmk_prerequisites"></a> Pré-requisitos  
  
-   Você deve ser um administrador local para executar a Instalação do SQL Server.  
  
-   O computador deve ser unido a um domínio.  
  
-   Você precisa saber o nome do servidor de banco de dados existente que está hospedando a configuração do SharePoint e os bancos de dados de conteúdo.  
  
-   O servidor de banco de dados deve ser configurado para permitir conexões de bancos de dados remotos.  Se não, você não poderá unir o novo servidor ao farm porque o novo servidor não poderá fazer uma conexão com os bancos de dados de configuração do SharePoint.  
  
-   O novo servidor precisará ter a mesma versão de SharePoint instalado que os servidores de farm atuais estão executando. Por exemplo, se o farm já tiver o SharePoint 2013 Service Pack 1 (SP1) instalado, você também precisará instalar o SP1 no novo servidor antes de unir o farm.  
  
##  <a name="bkmk_steps"></a> Etapas  
 As etapas neste tópico pressupõem que um administrador de farm do SharePoint esteja instalando e configurando o servidor. O diagrama mostra um ambiente típico de três camadas e os itens numerados no diagrama são descritos na lista a seguir:  
  
-   (1) Vários servidores de front-end da Web (WFE). Os servidores WFE exigem o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2016.  
  
-   (2) Um único servidor de aplicativos que executa o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e sites, por exemplo a Administração Central. As etapas a seguir adicionam um segundo servidor de aplicativos a esta camada.  
  
-   (3) Dois servidores de banco de dados do SQL Server.  
  
-   (4) Representa uma solução de software ou hardware de NLB (balanceamento de carga de rede)  
  
 ![Adicionar um servidor de aplicativos do Reporting Services](../../reporting-services/install-windows/media/rs-sharepointscale.gif "Adicionar um servidor de aplicativos do Reporting Services")  
  
 As etapas a seguir pressupõem que um administrador esteja instalando e configurando o servidor. O servidor será instalado como um novo servidor de aplicativos no farm e não usado como um WFE (front-end da Web).  
  
|Etapa|Descrição e link|  
|----------|--------------------------|  
|Adicione um servidor do SharePoint a um farm.|Você precisará instalar o SharePoint para implantar outro aplicativo do Reporting Services.<br/><br/>Para o SharePoint 2013, consulte [Adicionar o SharePoint Server a um farm no SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx).<br/><br/>Para o SharePoint 2016, consulte [Adicionar o SharePoint Server a um farm no SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx).|  
|Instalar e configurar o modo do SharePoint do Reporting Services.|Execute a instalação do SQL Server. Para obter mais informações sobre a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do modo do SharePoint, veja [Instalar o primeiro servidor de relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md)<br /><br /> Se o servidor for usado somente como um servidor de aplicativos e não como um WFE, você não precisará selecionar o **Suplemento do Reporting Services para produtos do SharePoint**.<br /><br /> 1) Na página **Função de instalação** , selecione **Instalação de recurso do SQL Server**<br /><br /> 2) Na página **Seleção de Recursos** , selecione **Reporting Services - SharePoint**<br /><br /> 3) Na página **Configuração do Reporting Services**  , verifique se a opção **Instalar somente** está marcada para o **Modo do SharePoint do Reporting Services**.|  
|Verifique se o Reporting Services está funcionando.|1) Na Administração Central do SharePoint, clique em **Gerenciar servidores neste farm** no grupo **Configurações do Sistema** .<br /><br /> 2) Verifique o serviço **SQL Server Reporting Services Service**.<br /><br />Para obter mais informações, consulte [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).|  
  
##  <a name="bkmk_additional"></a> Configuração adicional  
 Você pode otimizar servidores individuais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma implantação em expansão para realizar somente processamento em segundo plano, para que eles não tenham que competir por recursos com execução interativa de relatório. O processamento em segundo plano inclui agendas, assinaturas e alertas de dados.  
  
 Para alterar o comportamento de servidores de relatórios individuais, defina **\<IsWebServiceEnable>** como falso no arquivo de configuração **RSreportServer.config**.  
  
 Por padrão, os servidores de relatório são configurados com \<IsWebServiceEnable> definido como TRUE. Quando todos os servidores forem configurados para TRUE, o interativo e em segundo plano terão a carga equilibrada em todos os nós no farm.  
  
 Se você configurar todos os servidores de relatório com \<IsWebServiceEnable> definido como False, verá uma mensagem de erro semelhante à seguinte quando tentar usar os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
      The Reporting Services Web Service is not enabled. Configure at least one instance of the Reporting Services SharePoint Service to have <IsWebServiceEnable> set to true. 
 
 Para obter mais informações, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  

## <a name="next-steps"></a>Próximas etapas

[Adicionar o SharePoint Server a um farm no SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)  
[Adicionar o SharePoint Server a um farm no SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
