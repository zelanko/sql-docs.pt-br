---
title: Configurar o portal da web | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c0c6cc27711140e96bbf4420e8de596af53ddfcd
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-web-portal"></a>Configurar o portal da web

o portal da web é um aplicativo de front-end da Web usado para exibir relatórios, gerenciar o conteúdo do servidor de relatório e conceder acesso a um servidor de relatório do modo nativo. o portal da web é instalado com o serviço Web servidor de relatório dentro da mesma instância de servidor de relatório e, opcionalmente, configurado se você selecionar o **instalar na configuração de modo nativo padrão** opção na instalação. Você também pode configurar o portal da web como uma tarefa pós-instalação. Este tópico fornece informações sobre a seguir os cenários de configuração do portal da web:

## <a name="prerequisites"></a>Pré-requisitos

Para usar o portal da web, você deve atender aos seguintes pré-requisitos:

- Você deve ter um servidor de relatórios minimamente configurado. Para obter mais informações sobre como configurar no mínimo um servidor de relatório, consulte [configurar um servidor de relatório](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md).

- É necessário que o servidor de relatório seja executado no modo nativo. Você não pode usar o portal da web com um servidor de relatório está configurado para modo integrado do SharePoint. No SQL Server 2012, você não pode alternar um servidor de relatório de um modo para outro. Para alterar o tipo de servidor de relatório que seu ambiente usa, instale o modo desejado do servidor de relatório e copie ou mova os itens de relatório para o novo servidor de relatório. Esse processo geralmente é denominado 'migração'. As etapas necessárias para migrar dependem do modo que você está migrando e a versão da qual você está migrando. Para obter mais informações, consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

- Você também deve ter o Internet Explorer 11 ou posterior com script habilitado. Para obter mais informações, veja [Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).

## <a name="configure-the-web-portal-to-use-the-default-url"></a>Configurar o portal da web para usar a URL padrão

O portal da web é um aplicativo Web que os usuários acessam em um navegador da Web. Você deve definir a URL usada para abrir o aplicativo em uma janela do navegador. A URL consiste em um nome de host, uma porta e um diretório virtual. Os valores padrão dessa URL incluem o nome de host e os valores de porta definidos para a URL do serviço Web Servidor de Relatório, mais o nome do diretório virtual de **relatórios** . Se você tiver uma instância nomeada, o diretório virtual será **reports_instance**, em que **instance** será o nome da instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

Por padrão, o portal da web do URL consiste em um nome de diretório virtual exclusivo e o nome de host e porta que está definido para o serviço Web servidor de relatório que é executado na mesma instância. Na maioria dos casos, o nome de host é o nome de rede do computador servidor de relatórios, mas também pode ser um endereço IP ou cabeçalho de host que resolva o computador. Para configurar o portal da web para usar a URL padrão, use o **URL do Portal Web** página de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ferramenta de configuração.

> [!TIP]
> Se você tentar acessar o portal da web em um computador remoto e receber mensagens de erro de conexão em seu navegador, uma causa comum é configurações de Firewall. Para obter instruções, veja [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>Para configurar o portal da web padrão URL e o diretório virtual

1. Abra a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e se conecte à instância do servidor de relatório.

2. No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ferramenta de configuração, selecione **URL do Portal Web** para abrir a página para configurar a URL.

3. Insira um nome de diretório virtual exclusivos para o portal da web.

4. Clique em **Aplicar**.

5. Se você estiver usando [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] ou Windows Server 2008, etapas adicionais podem ser necessárias antes de usar o portal da web. Para obter mais informações, veja [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>Configurar o portal da web para usar uma URL do servidor de relatório específico

Por padrão, o portal da web se conecta ao serviço Web servidor de relatório que é executado no mesmo serviço de servidor de relatório. O portal da web usa a URL do serviço Web servidor de relatório para fazer a conexão. Se você definir várias URLs para o serviço Web do servidor de relatório, o portal da web usa o último deles que você definiu. No entanto, para algumas implantações, talvez você queira o portal da web para sempre se conectar ao serviço Web por meio de uma URL estática. Um exemplo de um motivo pelo qual talvez você queira fazer isso seria se tivesse configurado a filtragem de pacotes em uma determinada porta ou endereço IP, e quisesse que todas as conexões com o servidor de relatórios passassem pelas regras de filtragem definidas.

Quando você configura as URLs no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ferramenta de configuração, o portal da web automaticamente detecta e usa todas as URLs novas e atualizadas para o servidor de relatório que é executado na mesma instância do servidor. Se a sua implantação exigir o uso de uma única URL estática para todas as solicitações do servidor de relatórios, você poderá especificar essa URL no arquivo RSReportServer.config.

#### <a name="to-configure-a-static-report-server-url"></a>Para configurar uma URL estática do servidor de relatório

1. Abra o arquivo **RSReportServer.config** em um editor de texto. Por padrão, ele está localizado em \Program Files\Microsoft msrs12 SQL. \< *instancename*> services\reportserver..  

2. Localize **ReportServerURL**.

3. Substitua-o pela URL da instância do servidor de relatórios.

4. Salve suas alterações e feche o arquivo.

Para obter mais informações sobre o arquivo de configuração, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) no [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).

## <a name="customize-styles-or-application-title"></a>Personalizar estilos ou o título do aplicativo

Você pode criar um pacote de marca personalizada para alterar as cores usadas no portal da web. Para obter mais informações, consulte [identidade visual do portal da web](../branding-the-web-portal.md)

#### <a name="to-modify-application-title"></a>Para modificar o título do aplicativo

1. Faça logon usando uma conta que com permissões de **Administrador de Sistema** no servidor de relatório.

2. Abra o Internet Explorer.

3. Insira um portal da web do URL. Por padrão, ele é http://\<**seu nome de servidor**> / relatórios, mas se você instalou o Reporting Services como uma instância nomeada, a URL padrão será http://\<**seu nome de servidor**> / reports\<**_instancename**>.

4. Selecione **Configurações de Site**.

5. Na guia **Geral** , em **Nome**, substitua **SQL Server Reporting Services** por outro nome.

6. Escolha **Aplicar**.

## <a name="next-steps"></a>Próximas etapas

[Portal da Web](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Suporte a navegador do Reporting Services](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[configurar uma URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Ativar ou desativar o relatório recursos de serviços](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[Gerenciar um servidor de relatório de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Configurar um servidor de relatório do modo nativo para administração Local](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
