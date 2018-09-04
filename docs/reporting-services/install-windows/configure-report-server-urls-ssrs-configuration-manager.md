---
title: Configurar as URLs do Servidor de Relatório (	Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- Report Server Windows service, virtual directories
- report servers [Reporting Services], virtual directories
- virtual directories [Reporting Services]
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
author: markingmyname
ms.author: maghan
ms.openlocfilehash: db96a1af36bea565d00587096dfdbbc925b1fedf
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43273734"
---
# <a name="configure-report-server-urls--ssrs-configuration-manager"></a>Configurar as URLs do servidor de relatório (Configuration Manager do SSRS)
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], as URLs são usadas para acessar o serviço Web do Servidor de Relatório e o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Antes de usar qualquer um dos aplicativos, você deve configurar, pelo menos, uma URL para o serviço Web e o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece valores padrão para as URLs de ambos os aplicativos que funcionam bem na maioria dos cenários de implantação, incluindo implantações lado a lado com outros serviços Web e aplicativos.  
  
-   Se você instalou a configuração padrão, foram criadas URLs automaticamente usando os valores padrão.  
  
-   Se você estiver usando a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar ou modificar as URLs, poderá aceitar os valores padrão para uma URL ou especificar valores personalizados. Aparecerá um link de teste da URL na página quando você definir a URL, de maneira que possa confirmar imediatamente se as configurações especificadas resultam em uma conexão válida. Para obter instruções passo a passo sobre como configurar e testar uma URL, veja [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
## <a name="defining-a-report-server-url"></a>Definindo uma URL do servidor de relatório  
 A URL identifica com precisão o local de uma instância de um aplicativo de servidor de relatório em sua rede. Quando você criar a URL de um servidor de relatório, deverá especificar as seguintes partes.  
  
|Parte|Descrição|  
|----------|-----------------|  
|Nome do host|Uma rede TCP/IP usa um endereço IP para identificar exclusivamente um dispositivo na rede. Há um endereço IP físico para cada placa de adaptador de rede instalada em um computador. Se o endereço IP for resolvido para um cabeçalho de host, você poderá especificar esse cabeçalho. Se estiver implantando o servidor de relatório em uma rede corporativa, você poderá usar o nome de rede do computador.|  
|Porta|Uma porta TCP é um ponto de extremidade no dispositivo. O servidor de relatório escutará solicitações em uma porta designada.|  
|Diretório virtual|Uma porta normalmente é compartilhada por vários serviços Web ou aplicativos. Por esse motivo, uma URL de servidor de relatório sempre inclui um diretório virtual que corresponde ao aplicativo que obtém a solicitação. Você deve especificar nomes de diretórios virtuais exclusivos para cada aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que escute no mesmo endereço IP e porta.|  
|Configurações SSL|As URLs no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser configuradas para usar um certificado SSL existente que você instalou anteriormente no computador. Para obter mais informações, veja [Configurar conexões SSL em um Servidor de Relatórios do Modo Nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
## <a name="default-urls"></a>URLs padrão  
 Quando você acessa um servidor de relatório ou o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] por meio de sua respectiva URL, a URL deve incluir o nome do host, não o endereço IP. Em uma rede TCP/IP, o endereço IP será resolvido para um nome de host (ou o nome de rede do computador). Se você usou os valores padrão para configurar URLs, deverá poder acessar o serviço Web Servidor de Relatório usando URLs que especifiquem o nome do computador ou localhost como o nome do host:  
  
-   `http://<computername>/reportserver`  
  
-   `http://localhost/reportserver`  
  
 As configurações que disponibilizam essas URLs aparecem na tabela a seguir. Esta tabela mostra os valores padrão que habilitam uma conexão do servidor de relatório por meio de URLs que incluem um nome de host:  
  
|Parte|Valor|Explicação|  
|----------|-----------|-----------------|  
|Endereço IP|Todos Atribuídos|O serviço de nome de domínio em sua rede resolve o nome do host na URL para o endereço IP do computador. Desde que o endereço IP seja especificado na URL que você definir, uma solicitação enviada para um host específico alcançará seu destino pretendido.|  
|Porta|80|A porta 80 é a padrão para conexões TCP/IP em um computador. Como o servidor de relatório está escutando na porta 80, você pode omitir o número da porta da URL. Se você especificar outra porta, deverá especificá-la na URL.|  
|Diretório virtual|ReportServer|Note que ambos os exemplos de URLs incluem o nome do diretório virtual. A menos que você personalize a definição da URL, sempre deverá especificar o nome do diretório virtual do aplicativo na URL.|  
  
> [!NOTE]  
>  Uma reserva de URL subjacente habilita qualquer nome de host válido a ser usado em uma URL. A ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cria uma reserva de URL em HTTP.SYS usando uma sintaxe que permite que variações do nome do host sejam resolvidas em uma instância específica do servidor de relatório. Para obter mais informações sobre reservas de URL, veja [Sobre reservas e registro de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).  
  
## <a name="server-side-permissions-on-a-report-server-url"></a>Permissões do lado do servidor em uma URL de servidor de relatório  
 As permissões em cada ponto de extremidade de URL são concedidas exclusivamente à conta de serviço do Servidor de Relatório. Apenas essa conta tem direitos para aceitar solicitações que são dirigidas às URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . DACLs (Listas de Controle de Acesso Discricionário) são criadas e mantidas para a conta quando você configura a identidade do serviço por meio da Instalação ou da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se você alterar a conta de serviço, a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] atualizará todas as reservas de URL que você criou para obter as novas informações da conta. Para obter mais informações, veja [Sintaxe de reserva de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md).  
  
## <a name="authenticating-client-requests-sent-to-a-report-server-url"></a>Autenticando solicitações de cliente enviadas a uma URL de servidor de relatório  
 Por padrão, o tipo de autenticação suportado nos pontos de extremidade de URL é a Autenticação do Windows. Essa é a extensão de segurança padrão. Se você estiver implementando um provedor de autenticação de Formulários ou personalizado, deverá modificar as configurações de autenticação no servidor de relatório. Se preferir, você também poderá alterar as configurações de Autenticação do Windows para que correspondam ao subsistema de autenticação usado em sua rede. Para obter mais informações, veja [Autenticação com o Servidor de Relatório](../../reporting-services/security/authentication-with-the-report-server.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="in-this-section"></a>Nesta seção  
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 Esse tópico fornece instruções para a configuração e a modificação de uma reserva de URL na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 [Sobre reservas e registro de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 As URLs são usadas para acessar aplicativos e relatórios. Esse tópico explica as URLs de aplicativos, as URLs padrão e como s reservas de URL e o registro funcionam no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Sintaxe de reserva de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 As reservas de URL padrão usadas pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são válidas para a maioria dos cenários. Entretanto, para restringir o acesso ou estender a implantação a fim de habilitar o acesso de Internet ou extranet, você poderá ter que personalizar as configurações para que se ajustem a seus requisitos. Esse tópico descreve a sintaxe de uma reserva de URL e fornece recomendações para a criação de reservas personalizadas para sua implantação.  
  
 [URLs em arquivos de configuração &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 O arquivo RSReportServer.config contém várias entradas para reservas de URL e as URLs usadas pela entrega de email do servidor de relatório e pelo [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] . Esse tópico resume os parâmetros de configuração de URL de maneira que você possa entender como eles são comparados.  
  
 [Reservas de URL para implantações do Servidor de Relatório com várias instâncias &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)  
 Quando você instala várias instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um único computador, aumenta a probabilidade de encontrar duplicação de URL quando uma URL for registrada. Para evitar esses erros, siga as recomendações neste tópico para a criação de reservas de URL específicas da instância.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 
