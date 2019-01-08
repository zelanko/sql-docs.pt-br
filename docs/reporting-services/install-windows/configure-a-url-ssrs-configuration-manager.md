---
title: Configurar uma URL (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 912f0473db120c9874e231334d1d393e18518c71
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202485"
---
# <a name="configure-a-url--ssrs-configuration-manager"></a>Configurar uma URL (Gerenciador de Configurações do SSRS)
  Antes de poder usar o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] ou o serviço Web Servidor de Relatório, é necessário configurar, pelo menos, uma URL para cada aplicativo. A configuração das URLs será obrigatória se você instalou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo “somente arquivos” (ou seja, selecionando a opção **Instalar, mas não configurar o servidor** na página Opções de Instalação do Servidor de Relatório do Assistente de Instalação). Se você instalou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na configuração padrão, as URLs já estarão configuradas para cada aplicativo.  
  
 Use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar as URLs. Todas as partes da URL são definidas nessa ferramenta. Diferente das versões anteriores, os sites do IIS (Serviços de Informações da Internet) não fornecem mais acesso a aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e nas versões posteriores.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece valores padrão que funcionam na maioria dos cenários de implantação, incluindo implantações lado a lado com outros serviços e aplicativos Web. As URLs padrão inserirão nomes de instância, minimizando o risco de conflitos de URL se você executar várias instâncias do servidor de relatório no mesmo computador.  
  
 Este tópico fornece instruções para as seguintes tarefas:  
  
-   Criar uma URL para o serviço Web Servidor de Relatório.  
  
-   Crie uma URL para o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].  
  
-   Configurar propriedades avançadas de URL para definir URLs adicionais.  
  
 Para obter mais informações sobre como as URLs são armazenadas e mantidas ou sobre problemas de interoperabilidade, veja [Sobre reservas e registro de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md) e [Instalar o Reporting Services e os Serviços de Informações da Internet lado a lado &#40;Modo Nativo do SSRS&#41;](../../reporting-services/install-windows/install-reporting-and-internet-information-services-side-by-side.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para revisar exemplos de URLs usadas frequentemente em uma instalação do Reporting Services, consulte [Exemplos de URLs](#URLExamples) neste tópico.  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de criar ou modificar uma URL, lembre-se dos seguintes pontos:  
  
-   Você deve ser um membro do grupo Administradores local no computador do servidor de relatório.  
  
-   Se o IIS estiver instalado no mesmo computador, verifique os nomes dos diretórios virtuais em qualquer site que use a porta 80. Se você vir quaisquer diretórios virtuais que usem os nomes padrão de diretório virtual do Reporting Services (isto é, "Reports" e "ReportServer"), escolha nomes de diretório virtual diferentes para as URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você configurar.  
  
-   Você deve usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar a URL. Não use um utilitário de sistema. Nunca modifique reservas de URL diretamente na seção **URLReservations** do arquivo RSReportServer.config. O uso da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é necessário para atualizar a reserva de URL subjacente que é armazenada internamente e sincronizar as configurações de URL armazenadas no arquivo RSReportServer.config.  
  
-   Escolha uma hora que tenha baixa atividade de relatório. Sempre que a reserva de URL for alterada, você poderá esperar que os domínios de aplicativo do serviço Web do Servidor de Relatório e do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] sejam reciclados.  
  
-   Para obter uma visão geral da construção de URL e do uso de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
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
  
5.  Especifique a porta. Porta 80 é a padrão, pois pode ser compartilhada com outros aplicativos. Para usar um número de porta personalizado, lembre-se de que sempre deverá especificá-lo na URL usada para acessar o servidor de relatório. Você pode usar as seguintes técnicas para localizar uma porta disponível:  
  
    -   Em um prompt de comando, digite o seguinte comando para retornar uma lista de portas TCP que estão sendo usadas:  
  
         `netstat -anp tcp`  
  
    -   Examine o artigo de Suporte da Microsoft, [Informações sobre atribuições de porta TCP/IP](https://support.microsoft.com/kb/174904), para ler sobre atribuições de porta TCP e as diferenças entre Portas Bem Conhecidas (0 a 1023), Portas Registradas (1024 a 49151) e Portas Dinâmicas ou Privadas (49152 a 65535).  
  
    -   Se você estiver usando o Firewall do Windows, deverá abrir a porta. Para obter instruções, consulte [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Se ainda não o fez, verifique se o IIS (se ele estiver instalado) não tem um diretório virtual com o mesmo nome que você planeja usar.  
  
7.  Se você instalou um certificado SSL, poderá selecioná-lo agora para associar a URL ao certificado SSL que está instalado em seu computador.  
  
8.  Opcionalmente, se você selecionar um certificado SSL, poderá especificar uma porta personalizada. O padrão é 443, mas você pode usar qualquer porta que estiver disponível.  
  
9. Clique em **Aplicar** para criar a URL.  
  
10. Teste a URL clicando no link na seção **URLs** da página. Observe que o banco de dados do servidor de relatório deve ser criado e configurado antes que você possa testar a URL. Para obter instruções, veja [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  

> [!NOTE]
>  Se você tiver Associações SSL existentes e Reservas de URL e desejar alterar a Associação de SSL, por exemplo usar um certificado diferente ou cabeçalho de host, é recomendado concluir as etapas a seguir na ordem:  
> 
>  1.  Primeiro remova todas as Reservas de URL.  
> 2.  Em seguida, remova todas as Associações SSL.  
> 3.  Em seguida, recrie as URLs e as associações SSL.  
> 
>  As etapas anteriores podem ser concluídas usando o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
> 
>  A Microsoft Windows dá suporte a uma associação para cada endereço IP para a combinação de porta. Se você configurar um servidor de relatório para usar um valor de cabeçalho de host específico e o certificado na combinação Porta para endereço IP também for emitido para um valor de cabeçalho de host diferente, você verá em seu navegador um aviso indicando que o certificado não corresponde à URL que está sendo usada.  
> 
>  Para corrigir o problema, exclua todas as associações e crie novas associações com configurações exclusivas ou configure os registros de URL do Reporting Services com curingas.
  
### <a name="to-create-a-url-reservation-for-the-includessrswebportalincludesssrswebportalmd"></a>Para criar uma reserva de URL para o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]  
  
1.  Abra a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e se conecte à instância do servidor de relatório.  
  
2.  Clique em **URL do Portal da Web**.  
  
3.  Especifique o diretório virtual. O [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] escuta no mesmo endereço IP e porta que o serviço Web Servidor de Relatório. Se você configurou o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para que aponte para um serviço Web Servidor de Relatório diferente, deverá modificar as configurações da URL do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] no arquivo RSReportServer.config.  
  
4.  Se você instalou um certificado SSL, poderá selecioná-lo para requerer que todas as solicitações para o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] sejam roteadas por HTTPS.  
  
     Opcionalmente, se você selecionar um certificado SSL, poderá especificar uma porta personalizada. O padrão é 443, mas você pode usar qualquer porta que estiver disponível.  
  
5.  Clique em **Aplicar** para criar a URL.  
  
6.  Teste a URL clicando no link na seção **URLs** da página.  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a>Definindo propriedades avançadas para especificar URLs adicionais  
 Você pode reservar várias URLs para o serviço Web do Servidor de Relatório ou o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] especificando diferentes portas ou nomes de host (um endereço IP ou um nome de cabeçalho de host que um servidor de nomes de domínio possa resolver para um endereço IP atribuído ao computador). Ao criar várias URLs, você pode configurar diferentes caminhos de acesso para a mesma instância do servidor de relatório. Por exemplo, para habilitar o acesso de intranet e extranet a um servidor de relatório, você poderia usar a URL padrão para acesso pela intranet e um nome de host totalmente qualificado adicional para acesso de extranet.  
  
-   `https://myserver01/reportserver`  
  
-   `https://www.adventure-works.com/reportserver`  
  
 Você não pode definir vários nomes de diretórios virtuais para a mesma instância de aplicativo. Cada instância de aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é mapeada para um único nome de diretório virtual. Se você tiver várias instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no mesmo computador, o nome do diretório virtual para um aplicativo deve incluir o nome da instância para assegurar que cada solicitação alcance seu destino pretendido.  
 
  **Cabeçalho de Host**  
 Se você já tiver um cabeçalho de host definido em um servidor de nome de domínio que seja resolvido para seu computador, poderá especificar esse cabeçalho de host em uma URL que você configure para acesso ao servidor de relatório.  
  
 Um cabeçalho de host é um nome exclusivo que permite que vários sites compartilhem um único endereço IP e porta. Os nomes de cabeçalho de host são mais fáceis de se lembrar e digitar que endereço IP e números de porta. Um exemplo de um nome de cabeçalho de host poderia ser www.adventure-works.com.  
  
 **Porta SSL**  
 Especifica a porta para conexões SSL. A porta padrão para SSL é 443.  
  
 **Certificado SSL**  
 Especifica o nome de um certificado SSL que você instalou neste computador. Se o certificado for mapeado para um curinga, você poderá usá-lo para uma conexão de servidor de relatório.  
  
 Especifica o nome do computador totalmente qualificado para o qual o certificado está registrado. O nome que você especificar deve ser idêntico ao nome para o qual o certificado está registrado.  
  
 Você deve ter um certificado instalado para que possa usar essa opção. Você também deve modificar o parâmetro de configuração UrlRoot no arquivo RSReportServer.config para que ele especifique o nome totalmente qualificado do computador para o qual o certificado está registrado. Para obter mais informações, veja [Configurar conexões SSL em um Servidor de Relatórios do Modo Nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-set-advanced-properties-on-a-url"></a>Para definir propriedades avançadas em uma URL  
  
1.  Na página **URL do Serviço Web** ou **URL do Portal da Web** , clique em **Avançado**.  
  
2.  Clique em **Adicionar**.  
  
3.  Clique em Endereço IP ou Nome de Cabeçalho do Host. Se você especificar um cabeçalho de host, certifique-se de especificar um nome que o serviço DNS possa resolver. Se você estiver especificando um nome de domínio disponível publicamente, inclua a URL inteira, incluindo `https://www`.  
  
4.  Especifique a porta. Se você especificar uma porta personalizada, a URL do aplicativo sempre deverá incluir o número da porta.  
  
5.  Clique em **OK**.  
  
6.  Teste a URL abrindo uma janela de navegador e digitando a URL.  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a>URLs para várias instâncias do Servidor de Relatório no mesmo computador  
 Se você estiver reservando URLs para várias instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], deverá seguir as convenções de nomenclatura para que possa evitar conflitos de nomenclatura. Para obter mais informações, veja [Reservas de URL para implantações do Servidor de Relatório com várias instâncias &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md).  
  
##  <a name="URLExamples"></a> Exemplos de configurações de URL  
 A lista a seguir mostra alguns exemplos de qual pode ser a aparência de uma URL de servidor de relatório:  
  
-   `https://localhost/reportserver`  
  
-   `https://localhost/reportserver_SQLEXPRESS`  
  
-   `https://sales01/reportserver`  
  
-   `https://sales01:8080/reportserver`  
  
-   `https://sales.adventure-works.com/reportserver`  
  
-   `https://www.adventure-works.com:8080/reportserver01`  
  
 As URLs usadas para acessar o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] compartilham um formato semelhante e normalmente são criadas no mesmo site que hospeda o servidor de relatório. A única diferença é o nome do diretório virtual (neste caso, ele é **reports** , mas você pode configurá-lo para usar qualquer nome que desejar):  
  
-   `https://localhost/reports`  
  
-   `https://localhost/reports_SQLEXPRESS`  
  
-   `https://sales01/reports`  
  
-   `https://sales01:8080/reports`  
  
-   `https://sales.adventure-works.com/reports`  
  
-   `https://www.adventure-works.com:8080/reports`  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)
