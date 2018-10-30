---
title: Configurar o portal da Web | Microsoft Docs
ms.date: 05/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f37cb519981b0f3ac0be532ad82e6ed74d073d8f
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50031693"
---
# <a name="configure-the-web-portal"></a>Configurar o portal da Web

o portal da Web é um aplicativo de front-end da Web usado para exibir relatórios, gerenciar o conteúdo do servidor de relatório e conceder acesso a um usuário ao servidor de relatório no modo nativo. o portal da Web é instalado com o serviço Web Servidor de Relatórios na mesma instância do servidor de relatório e, opcionalmente, configurado se você selecionar a opção **Instalar na configuração de modo nativo padrão** na Instalação. Também é possível configurar o portal da Web como uma tarefa pós-instalação. Este tópico fornece informações sobre os seguintes cenários de configuração do portal da Web:

## <a name="prerequisites"></a>Prerequisites

Para usar o portal da Web, é necessário atender aos seguintes pré-requisitos:

- Você deve ter um servidor de relatórios minimamente configurado. Para obter mais informações sobre como definir um servidor de relatório com as configurações mínimas, consulte [Configurar um servidor de relatório](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md).

- É necessário que o servidor de relatório seja executado no modo nativo. Não é possível usar o portal da Web com um servidor de relatório configurado para o modo integrado do SharePoint. No SQL Server 2012, você não pode alternar um servidor de relatório de um modo para outro. Para alterar o tipo de servidor de relatório que seu ambiente usa, instale o modo desejado do servidor de relatório e copie ou mova os itens de relatório para o novo servidor de relatório. Esse processo geralmente é denominado 'migração'. As etapas necessárias para migrar dependem do modo que você está migrando e a versão da qual você está migrando. Para obter mais informações, consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

- Você também deve ter o Internet Explorer 11 ou posterior com script habilitado. Para obter mais informações, veja [Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).

## <a name="configure-the-web-portal-to-use-the-default-url"></a>Configurar o portal da Web para usar a URL padrão

O portal da Web é um aplicativo Web que os usuários acessam em um navegador da Web. Você deve definir a URL usada para abrir o aplicativo em uma janela do navegador. A URL consiste em um nome de host, uma porta e um diretório virtual. Os valores padrão dessa URL incluem o nome de host e os valores de porta definidos para a URL do serviço Web Servidor de Relatório, mais o nome do diretório virtual de **relatórios** . Se você tiver uma instância nomeada, o diretório virtual será **reports_instance**, em que **instance** será o nome da instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

Por padrão, a URL do portal da Web consiste em um nome de diretório virtual exclusivo, mais a porta e o nome do host definidos para o serviço Web Servidor de Relatórios executado na mesma instância. Na maioria dos casos, o nome de host é o nome de rede do computador servidor de relatórios, mas também pode ser um endereço IP ou cabeçalho de host que resolva o computador. Para configurar o portal da Web para usar a URL padrão, use a página **URL do Portal da Web** na ferramenta de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

> [!TIP]
> Se você tentar acessar o portal da Web em um computador remoto e receber mensagens de erro de conexão no navegador, uma causa comum serão as configurações do firewall. Para obter instruções, veja [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>Para configurar a URL padrão e o diretório virtual do portal da Web

1. Abra a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e se conecte à instância do servidor de relatório.

2. Na ferramenta de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], selecione **URL do Portal da Web** para abrir a página para configurar a URL.

3. Insira um nome de diretório virtual exclusivo para o portal da Web.

4. Clique em **Aplicar**.

5. Se estiver usando o [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] ou o Windows Server 2008, talvez sejam necessárias algumas etapas adicionais antes de usar o portal da Web. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>Configurar o portal da Web para usar uma URL específica do servidor de relatório

Por padrão, o portal da Web se conecta ao serviço Web Servidor de Relatórios executado no mesmo serviço Servidor de Relatórios. O portal da Web usa a URL do serviço Web Servidor de Relatórios para estabelecer a conexão. Se você definir várias URLs para o serviço Web Servidor de Relatórios, o portal da Web usará a última URL definida. No entanto, para algumas implantações, talvez você deseje que o portal da Web sempre se conecte ao serviço Web por meio de uma URL estática. Um exemplo de um motivo pelo qual talvez você queira fazer isso seria se tivesse configurado a filtragem de pacotes em uma determinada porta ou endereço IP, e quisesse que todas as conexões com o servidor de relatórios passassem pelas regras de filtragem definidas.

Quando você configura as URLs na ferramenta de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o portal da Web detecta e usa automaticamente todas as URLs novas e atualizadas do servidor de relatório executado na mesma instância do servidor. Se a sua implantação exigir o uso de uma única URL estática para todas as solicitações do servidor de relatórios, você poderá especificar essa URL no arquivo RSReportServer.config.

#### <a name="to-configure-a-static-report-server-url"></a>Para configurar uma URL estática do servidor de relatório

1. Abra o arquivo **RSReportServer.config** em um editor de texto. Por padrão, ele está localizado em \Program Files\Microsoft SQL Server\MSRS12.\<*instancename*>\Reporting Services\ReportServer.  

2. Localize **ReportServerURL**.

3. Substitua-o pela URL da instância do servidor de relatórios.

4. Salve suas alterações e feche o arquivo.

Para obter mais informações sobre o arquivo de configuração, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) no [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).

## <a name="customize-styles-or-application-title"></a>Personalizar estilos ou o título do aplicativo

Crie um pacote de marca personalizada para alterar as cores usadas no portal da Web. Para obter mais informações, consulte [Criando uma identidade visual para o portal da Web](../branding-the-web-portal.md)

#### <a name="to-modify-application-title"></a>Para modificar o título do aplicativo

1. Faça logon usando uma conta que com permissões de **Administrador de Sistema** no servidor de relatório.

2. Abra o Internet Explorer.

3. Insira a URL do portal da Web. Por padrão, considera-se http://\<**your-server-name**>/reports, mas se você tiver instalado o Reporting Services como uma instância nomeada, a URL padrão será http://\<**your-server-name**>/reports\<**_instancename**>.

4. Selecione **Configurações de Site**.

5. Na guia **Geral** , em **Nome**, substitua **SQL Server Reporting Services** por outro nome.

6. Escolha **Aplicar**.

## <a name="next-steps"></a>Próximas etapas

[Portal da Web](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Suporte a navegador do Reporting Services](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[Configurar uma URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Ativar e desativar recursos do Reporting Services](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[Gerenciar um servidor de relatório de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Configurar um servidor de relatório no modo nativo para administração local](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
