---
title: Configurar uma URL (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7ab343a4c6f70d97aa5e770b8ca21dd4d835f05c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375928"
---
# <a name="configure-a-url--ssrs-configuration-manager"></a>Configurar uma URL (Gerenciador de Configurações do SSRS)
  Antes de usar o Gerenciador de Relatórios ou o serviço Web Servidor de Relatório, você deve configurar pelo menos uma URL para cada aplicativo. A configuração das URLs será obrigatória se você instalou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo "somente arquivos" (isto é, selecionando a opção **Instalar, mas não configurar o servidor** na página Opções de Instalação do Servidor de Relatório do Assistente de Instalação). Se você instalou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na configuração padrão, as URLs já estarão configuradas para cada aplicativo. Caso você tenha um servidor de relatório configurado para usar o modo Integrado do SharePoint e atualize a URL do Serviço Web Servidor de Relatórios usando a ferramenta de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , também deverá atualizar a URL na Administração Central do SharePoint.  
  
 Use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar as URLs. Todas as partes da URL são definidas nessa ferramenta. Diferente das versões anteriores, os sites do IIS (Serviços de Informações da Internet) não fornecem mais acesso a aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e nas versões posteriores.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece valores padrão que funcionam na maioria dos cenários de implantação, incluindo implantações lado a lado com outros serviços e aplicativos Web. As URLs padrão inserirão nomes de instância, minimizando o risco de conflitos de URL se você executar várias instâncias do servidor de relatório no mesmo computador.  
  
 Este tópico fornece instruções para as seguintes tarefas:  
  
-   Criar uma URL para o serviço Web Servidor de Relatório.  
  
-   Criar uma URL para o Gerenciador de Relatórios.  
  
-   Configurar propriedades avançadas de URL para definir URLs adicionais.  
  
 Para obter mais informações sobre como as URLs são armazenadas e mantidas ou sobre problemas de interoperabilidade, consulte [sobre reservas de URL e registro de &#40;Configuration Manager do SSRS&#41; ](about-url-reservations-and-registration-ssrs-configuration-manager.md) e [Install Reporting Serviços de informações da Internet e os serviços lado a lado &#40;modo nativo do SSRS&#41;](install-reporting-and-internet-information-services-side-by-side.md)na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online. Para revisar exemplos de URLs usadas frequentemente em uma instalação do Reporting Services, consulte [Exemplos de URLs](#URLExamples) neste tópico.  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de criar ou modificar uma URL, lembre-se dos seguintes pontos:  
  
-   Você deve ser um membro do grupo Administradores local no computador do servidor de relatório.  
  
-   Se o IIS 6.0 ou 7.0 estiver instalado no mesmo computador, verifique os nomes dos diretórios virtuais em qualquer site que use a porta 80. Se você vir quaisquer diretórios virtuais que usem os nomes padrão de diretório virtual do Reporting Services (isto é, "Reports" e "ReportServer"), escolha nomes de diretório virtual diferentes para as URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você configurar.  
  
-   Você deve usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar a URL. Não use um utilitário de sistema. Nunca modifique reservas de URL diretamente na seção `URLReservations` do arquivo RSReportServer.config. O uso da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é necessário para atualizar a reserva de URL subjacente que é armazenada internamente e sincronizar as configurações de URL armazenadas no arquivo RSReportServer.config.  
  
-   Escolha uma hora que tenha baixa atividade de relatório. Toda vez que a reserva de URL for alterada, você pode esperar que os domínios de aplicativo do serviço Web Servidor de Relatório e do Gerenciador de Relatórios sejam reciclados.  
  
-   Para obter uma visão geral da construção de URL e do uso de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](configure-report-server-urls-ssrs-configuration-manager.md).  
  
### <a name="to-configure-a-url-for-the-report-server-web-service"></a>Para configurar uma URL para serviço Web Servidor de Relatório  
  
1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se a uma instância local do servidor de relatório.  
  
2.  Clique em **URL do Serviço Web**.  
  
3.  Especifique o diretório virtual. O nome do diretório virtual identifica qual aplicativo recebe a solicitação. Como um endereço IP e uma porta podem ser compartilhados por vários aplicativos, o nome do diretório virtual especifica qual aplicativo recebe a solicitação.  
  
     Esse valor deve ser exclusivo para assegurar que a solicitação alcance seu destino planejado. Esse valor é necessário. Ele não diferencia maiúsculas e minúsculas. Há uma correspondência um para um entre um nome de diretório virtual e uma instância de um aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se você criar várias URLs para a mesma instância de aplicativo, deverá usar o mesmo nome de diretório virtual em todas as URLs definidas para essa instância de aplicativo.  
  
     Para o serviço Web Servidor de Relatório, o nome padrão do diretório virtual é **ReportServer**.  
  
4.  Especifique o endereço IP identifica exclusivamente o computador do servidor de relatório na rede. Para especificar um cabeçalho de host ou definir URLs adicionais para a mesma instância de aplicativo, você deve clicar em **Avançado**. Para obter instruções sobre como definir propriedades avançadas na URL, consulte as instruções posteriormente neste tópico. Caso contrário, use a página **URL do Serviço Web** para selecionar entre os seguintes valores:  
  
    -   **Todos Atribuídos** especifica que qualquer um dos endereços IP atribuídos ao computador podem ser usados em uma URL que aponta para um aplicativo do servidor de relatório. Esse valor também abrange nomes de host amigáveis (como nomes de computadores) que podem ser resolvidos por um servidor de nome de domínio para um endereço IP que é atribuído ao computador. Esse é o valor padrão para uma URL do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    -   **Nenhum Atribuído** especifica que o servidor de relatório receberá qualquer solicitação que não foi tratada por outro aplicativo. Recomenda-se que você evite essa opção. Se você selecionar essa opção, será possível que outro aplicativo que tenha uma reserva de URL mais forte intercepte solicitações destinadas ao servidor de relatório.  
  
    -   **127.0.0.1** é o endereço IPv4 usado para acesso a localhost. Ele dá suporte à administração local no computador do servidor de relatório. Se você selecionar apenas esse valor, somente os usuários que fizerem logon localmente no computador do servidor de relatório terão acesso ao aplicativo.  
  
    -   **::1** é o endereço de loopback no formato IPv6.  
  
    -   Endereços IP específicos também aparecem nessa lista. Os endereços IP podem estar nos formatos IPv4 e IPv6. *Nnn.nnn.nnn.nnn* é o endereço IPv4 de 32 bits de uma placa de adaptador de rede em seu computador. Os endereços IPv6 são de 128 bits, com oito campos de 4 bytes separados por dois-pontos: \<prefix>:*nnnn:nnnn:nnnn:nnnn:nnnn:nnnn*  
  
         Se você tiver várias placas ou se a sua rede der suporte a endereços IPv4 e IPv6, você verá vários endereços IP. Se você selecionar apenas um endereço IP, isso limitará o acesso do aplicativo somente ao endereço IP (e qualquer nome de host que um servidor de nome de domínio mapear para esse endereço). Você não pode usar localhost para acessar um servidor de relatório e não pode usar os endereços IP de outras placas de adaptador de rede que estejam instaladas no computador do servidor de relatório. Normalmente, se você selecionar esse valor, é porque está configurando várias reservas de URL que também especificam endereços IP explícitos ou nomes de host (por exemplo, uma para uma placa de adaptador de rede usada para conexões à intranet e uma segunda usada para conexões à extranet).  
  
5.  Especifique a porta. A porta 80 é a padrão para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] e no Windows Server 2008 porque ela pode ser compartilhada com outros aplicativos. Para usar um número de porta personalizado, lembre-se de que sempre deverá especificá-lo na URL usada para acessar o servidor de relatório. Você pode usar as seguintes técnicas para localizar uma porta disponível:  
  
    -   Em um prompt de comando, digite o seguinte comando para retornar uma lista de portas TCP que estão sendo usadas:  
  
         `netstat -a -n -p tcp`  
  
    -   Examine o artigo de Suporte da Microsoft, [Informações sobre atribuições de porta TCP/IP](https://support.microsoft.com/kb/174904), para ler sobre atribuições de porta TCP e as diferenças entre Portas Bem Conhecidas (0 a 1023), Portas Registradas (1024 a 49151) e Portas Dinâmicas ou Privadas (49152 a 65535).  
  
    -   Se você estiver usando o Firewall do Windows, deverá abrir a porta. Para obter instruções, consulte [Configure a Firewall for Report Server Access](../report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Se ainda não o fez, verifique se o IIS (se ele estiver instalado) não tem um diretório virtual com o mesmo nome que você planeja usar.  
  
7.  Se você instalou um certificado SSL, poderá selecioná-lo agora para associar a URL ao certificado SSL que está instalado em seu computador.  
  
8.  Opcionalmente, se você selecionar um certificado SSL, poderá especificar uma porta personalizada. O padrão é 443, mas você pode usar qualquer porta que estiver disponível.  
  
9. Clique em **Aplicar** para criar a URL.  
  
10. Teste a URL clicando no link na seção **URLs** da página. Observe que o banco de dados do servidor de relatório deve ser criado e configurado antes que você possa testar a URL. Para obter instruções, consulte [Criar um banco de dados de servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
11. Além disso, se o servidor de relatório estiver configurado para usar o modo Integrado do SharePoint, configure a URL do serviço Web Servidor de Relatórios na Administração Central do SharePoint. Para obter mais informações sobre como atualizar a URL do serviço Web servidor de relatório na Administração Central do SharePoint, consulte [configuração e administração de um servidor de relatório &#40;Reporting Services SharePoint Mode&#41; ](../configure-administer-report-server-reporting-services-sharepoint-mode.md) e [Reporting Services Report Server &#40;modo do SharePoint&#41;](../reporting-services-report-server-sharepoint-mode.md).  
  
### <a name="to-create-a-url-reservation-for-report-manager"></a>Para criar uma reserva de URL para o Gerenciador de Relatórios  
  
1.  Abra a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e se conecte à instância do servidor de relatório.  
  
2.  Clique em **URL do Gerenciador de Relatórios**.  
  
3.  Especifique o diretório virtual. O Gerenciador de Relatórios escuta no mesmo endereço IP e porta que o serviço Web Servidor de Relatório. Se você configurou o Gerenciador de Relatórios para que aponte para um serviço Web Servidor de Relatório diferente, deverá modificar as configurações da URL do Gerenciador de Relatórios no arquivo RSReportServer.config. Para obter instruções, consulte [configurar o Gerenciador de relatórios &#40;modo nativo&#41; ](../report-server/configure-web-portal.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
4.  Se você instalou um certificado SSL, poderá selecioná-lo para requerer que todas as solicitações para o Gerenciador de Relatórios sejam roteadas por HTTPS.  
  
     Opcionalmente, se você selecionar um certificado SSL, poderá especificar uma porta personalizada. O padrão é 443, mas você pode usar qualquer porta que estiver disponível.  
  
5.  Clique em **Aplicar** para criar a URL.  
  
6.  Teste a URL clicando no link na seção **URLs** da página.  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a>Definindo propriedades avançadas para especificar URLs adicionais  
 Você pode reservar várias URLs para o serviço Web Servidor de Relatório ou o Gerenciador de Relatórios especificando diferentes portas ou nomes de host (um endereço IP ou um nome de cabeçalho de host que um servidor de nome de domínio possa resolver para um endereço IP atribuído ao computador). Ao criar várias URLs, você pode configurar diferentes caminhos de acesso para a mesma instância do servidor de relatório. Por exemplo, para habilitar o acesso de intranet e extranet a um servidor de relatório, você poderia usar a URL padrão para acesso pela intranet e um nome de host totalmente qualificado adicional para acesso de extranet.  
  
-   http://myserver01/reportserver  
  
-   http://www.adventure-works.com/reportserver  
  
 Você não pode definir vários nomes de diretórios virtuais para a mesma instância de aplicativo. Cada instância de aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é mapeada para um único nome de diretório virtual. Se você tiver várias instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no mesmo computador, o nome do diretório virtual para um aplicativo deve incluir o nome da instância para assegurar que cada solicitação alcance seu destino pretendido.  
  
#### <a name="to-set-advanced-properties-on-a-url"></a>Para definir propriedades avançadas em uma URL  
  
1.  Na página **URL do Serviço Web** ou **URL do Gerenciador de Relatórios** , clique em **Avançado**.  
  
2.  Clique em **Adicionar**.  
  
3.  Clique em Endereço IP ou Nome de Cabeçalho do Host. Se você especificar um cabeçalho de host, certifique-se de especificar um nome que o serviço DNS possa resolver. Se você estiver especificando um nome de domínio disponível publicamente, inclua a URL inteira, incluindo http://www.  
  
4.  Especifique a porta. Se você especificar uma porta personalizada, a URL do aplicativo sempre deverá incluir o número da porta.  
  
5.  Clique em **OK**.  
  
6.  Teste a URL abrindo uma janela de navegador e digitando a URL.  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a>URLs para várias instâncias do Servidor de Relatório no mesmo computador  
 Se você estiver reservando URLs para várias instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], deverá seguir as convenções de nomenclatura para que possa evitar conflitos de nomenclatura. Para obter mais informações, veja [Reservas de URL para implantações do Servidor de Relatório com várias instâncias &#40;SSRS Configuration Manager&#41;](url-reservations-for-multi-instance-report-server-deployments.md).  
  
##  <a name="URLExamples"></a> Exemplos de configurações de URL  
 A lista a seguir mostra alguns exemplos de qual pode ser a aparência de uma URL de servidor de relatório:  
  
-   http://localhost/reportserver  
  
-   http://localhost/reportserver_SQLEXPRESS  
  
-   http://sales01/reportserver  
  
-   http://sales01:8080/reportserver  
  
-   https://sales.adventure-works.com/reportserver  
  
-   https://www.adventure-works.com:8080/reportserver01  
  
 As URLs usadas para acessar o Gerenciador de Relatórios compartilham um formato semelhante e normalmente são criadas no mesmo site que hospeda o servidor de relatório. A única diferença é o nome do diretório virtual (neste caso, ele é **reports** , mas você pode configurá-lo para usar qualquer nome que desejar):  
  
-   http://localhost/reports  
  
-   http://localhost/reports_SQLEXPRESS  
  
-   http://sales01/reports  
  
-   http://sales01:8080/reports  
  
-   https://sales.adventure-works.com/reports  
  
-   https://www.adventure-works.com:8080/reports  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
