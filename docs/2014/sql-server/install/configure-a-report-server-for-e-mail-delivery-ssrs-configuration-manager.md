---
title: Configurar um servidor de relatório para entrega de email (Gerenciador de configuração do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], distributing
- report servers [Reporting Services], e-mail delivery
- remote SMTP service [Reporting Services]
- distributing reports [Reporting Services], e-mail
- CDO
- Collaboration Data Objects
- SMTP settings [Reporting Services]
- e-mail [Reporting Services]
- sending reports
- mail [Reporting Services]
- local SMTP service [Reporting Services]
ms.assetid: b838f970-d11a-4239-b164-8d11f4581d83
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e189890845bad34153ebef4231465c260b538848
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179193"
---
# <a name="configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager"></a>Configurar um servidor de relatório para entrega de email (Gerenciador de Configurações do SSRS)
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email, para que você possa distribuir relatórios por email. Dependendo de como você definir a assinatura de email, uma entrega pode consistir em uma notificação, um link, um anexo ou um relatório inserido. A extensão de entrega de email funciona com sua tecnologia de servidor de email existente. O servidor de email deve ser um encaminhador ou servidor SMTP. O servidor de relatório se conecta a um servidor SMTP por meio de bibliotecas (cdosys.dll) de CDO (Collaboration Data Objects) que são fornecidas pelo sistema operacional.  
  
 A extensão de entrega de email do servidor de relatório não é configurada por padrão. Você deve usar o Gerenciador de Configurações do Reporting Services para configurar a extensão de forma mínima. Para definir propriedades avançadas, você deve editar o arquivo `RSReportServer.config` . Se não for possível configurar o servidor de relatório para usar essa extensão, em vez disso você poderá entregar relatórios para uma pasta compartilhada. Para obter mais informações, consulte [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
 
  
##  <a name="bkmk_configuration_requirements"></a> Requisitos de configuração  
  
-   A entrega de email do servidor de relatório é implementada em CDO (Collaboration Data Objects) e requer um servidor SMTP local ou remoto ou um encaminhador SMTP. Não há suporte ao SMTP em todos os sistemas operacionais Windows. Se você estiver usando a edição com base em Itanium do Windows Server 2008, não haverá suporte ao SMTP. Para obter mais informações sobre as opções de configuração fornecidas por CDO, consulte [Configuration CoClass](http://go.microsoft.com/fwlink/?LinkId=98237) (em inglês) no MSDN.  
  
-   Uma conta de serviço do Servidor de Relatório deve ter permissão no servidor SMTP para enviar email.  
  
-   A extensão de entrega de email usa a codificação UTF-8 em anexos de email. Você não pode modificar a codificação; a extensão de renderização HTML só dá suporte a UTF-8.  
  
> [!NOTE]  
>  A extensão de entrega de email padrão não dá suporte para assinar digitalmente ou criptografar mensagens de email de saída.  
  
 
  
##  <a name="bkmk_configure_for_local_or_remote_SMTP"></a> Configurando um servidor de relatório para o serviço SMTP Local ou remoto  
 Você pode usar um serviço SMTP local ou um encaminhador ou servidor SMTP remoto para suportar entrega de email. Se tiver acesso a um servidor SMTP remoto existente, você deverá considerar seu uso. Se não houver nenhum servidor SMTP disponível ou se subsequentemente você encontrar erros de entrega de relatório que possam ser atribuídos a falhas de conexão do computador, você deverá alternar para o uso de um serviço SMTP local. Detalhes sobre como configurar um servidor de relatório para serviço local ou remoto são fornecidos mais adiante neste tópico.  
  
  
  
##  <a name="bkmk_setting_email_delivery"></a> Opções de configuração para entrega de email  
 Antes de usar a entrega de email do Servidor de Relatório, você deve definir valores de configuração que forneçam informações sobre qual servidor SMTP será usado.  
  
 Para configurar um servidor de relatório para entrega de email, faça o seguinte:  
  
-   Use o Gerenciador de Configurações do Reporting Services se estiver especificando somente um servidor SMTP e uma conta de usuário que tenha permissão para enviar email. Essas são as configurações mínimas necessárias para a configuração da extensão de entrega de email do Servidor de Relatório. Para obter mais informações, consulte [configurações de email – Configuration Manager &#40;modo nativo do SSRS&#41; ](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) e [entrega de email no Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   (Opcionalmente) Use um editor de texto para especificar configurações adicionais no arquivo RSreportserver.config. Esse arquivo contém todos os parâmetros de configuração para a entrega de email do Servidor de Relatório. Será necessário especificar configurações adicionais nesses arquivos se você estiver usando um servidor SMTP local ou se estiver restringindo a entrega de email para hosts específicos. Para obter mais informações sobre como localizar e modificar arquivos de configuração, consulte [modificar um arquivo de configuração do Reporting Services &#40;rsreportserver. config&#41; ](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do SQL Server.  
  
> [!NOTE]  
>  As configurações de email do servidor de relatório têm como base o CDO. Para obter mais detalhes sobre configurações específicas, você pode consultar a documentação de produção do CDO.  
  

  
##  <a name="bkmk_example_config_file"></a> Configuração de email do servidor de relatório de exemplo  
 O exemplo a seguir ilustra as configurações no arquivo RSreportserver.config para um servidor SMTP remoto. Para ler sobre as descrições de configuração e valores válidos, consulte [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os Manuais Online ou a documentação do produto CDO.  
  
```  
<RSEmailDPConfiguration>  
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>  
     <SMTPServerPort></SMTPServerPort>  
     <SMTPAccountName></SMTPAccountName>  
     <SMTPConnectionTimeout></SMTPConnectionTimeout>  
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>  
     <SMTPUseSSL></SMTPUseSSL>  
     <SendUsing>2</SendUsing>  
     <SMTPAuthenticate></SMTPAuthenticate>  
     <From>my-rs-email-account@Adventure-Works.com</From>  
     <EmbeddedRenderFormats>  
          <RenderingExtension>MHTML</RenderingExtension>  
     </EmbeddedRenderFormats>  
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>  
     <ExcludedRenderFormats>  
          <RenderingExtension>HTMLOWC</RenderingExtension>  
          <RenderingExtension>NULL</RenderingExtension>  
     </ExcludedRenderFormats>  
     <SendEmailToUserAlias>True</SendEmailToUserAlias>  
     <DefaultHostName></DefaultHostName>  
     <PermittedHosts>  
          <HostName>Adventure-Works.com</HostName>  
          <HostName>hotmail.com</HostName>  
     </PermittedHosts>  
</RSEmailDPConfiguration>  
```  
  

  
##  <a name="bkmk_setting_TO_field"></a> Opções de configuração para a configuração de para: campo em uma mensagem  
 As assinaturas definidas pelo usuário que forem criadas de acordo com as permissões concedidas pela tarefa **Gerenciar assinaturas individuais** contêm um nome de usuário predefinido que tem como base a conta de usuário do domínio. Quando o usuário cria a assinatura, o nome do destinatário no campo **Para:** é endereçado a si mesmo, usando a conta do usuário do domínio da pessoa que está criando a assinatura.  
  
 Se você estiver usando um servidor ou encaminhador SMTP que use contas de email diferentes da conta de usuário do domínio, a entrega do relatório falhará quando o servidor SMTP tentar entregar o relatório para esse usuário.  
  
 Para solucionar esse erro, você pode modificar os parâmetros de configuração que permitem aos usuários inserir um nome no campo **Para:** :  
  
1.  Abra RSReportServer.config com um editor de texto.  
  
2.  Definir `SendEmailToUserAlias` para `False`.  
  
3.  Definir `DefaultHostName` para o sistema de nome de domínio (DNS) ou endereço IP do encaminhador ou servidor SMTP.  
  
4.  Salve o arquivo.  
  
  
  
##  <a name="bkmk_options_remote_SMTP"></a> Opções de configuração para o serviço SMTP remoto  
 A conexão entre o servidor de relatório e um encaminhador ou servidor SMTP é determinada pelos seguintes parâmetros de configuração:  
  
-   `SendUsing` Especifica um método para enviar mensagens. Você pode escolher entre um serviço de rede SMTP ou um diretório local de retirada de serviço SMTP. Para usar um serviço SMTP remoto, este valor deve ser definido como **2** no arquivo RSReportServer.config.  
  
-   `SMTPServer` Especifica o encaminhador ou servidor SMTP remoto. Esse valor será necessário se você estiver usando um encaminhador ou servidor SMTP remoto.  
  
-   `From` Define o valor que aparece na **de:** linha de uma mensagem de email. Esse valor será necessário se você estiver usando um encaminhador ou servidor SMTP remoto.  
  
 Outros valores usados para o serviço SMTP remoto incluem os seguintes (observe que não é necessário especificar esses valores, a menos que deseje substituir os valores padrão).  
  
-   **SMTPServerPort** é configurado para a porta 25.  
  
-   **SMTPAuthenticate** especifica como o servidor de relatório se conecta ao servidor SMTP remoto. O valor padrão é 0 (sem autenticação). Nesse caso, a conexão é feita por acesso Anônimo. Dependendo da configuração do domínio, o servidor de relatório e o servidor SMTP podem precisar ser membros do mesmo domínio.  
  
     Para enviar e-mail para listas de distribuição restritas (por exemplo, listas de distribuição que aceitem mensagens de entrada apenas de contas autenticadas), defina **SMTPAuthenticate** como **2**.  
  

  
##  <a name="bkmk_options_local_SMTP"></a> Opções de configuração para o serviço SMTP Local  
 A configuração de um serviço SMTP local será útil se você estiver testando ou solucionando problemas de entrega de email do servidor de relatório. O serviço SMTP local não está habilitado por padrão. Para obter instruções sobre como habilitá-lo, consulte [configurar um servidor de relatório para entrega de email (Gerenciador de configuração do SSRS)](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [configurações de email – Configuration Manager &#40;modo nativo do SSRS&#41; ](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) .  
  
 A conexão entre o servidor de relatório e um encaminhador ou servidor SMTP local é determinada pelos seguintes parâmetros de configuração:  
  
-   `SendUsing` é definido como **1**.  
  
-   **SMTPServerPickupDirectory** é definido como uma pasta na unidade local.  
  
    > [!NOTE]  
    >  Certifique-se de que você não defina `SMTPServer` se você estiver usando um servidor SMTP local.  
  
-   `From` Define o valor que aparece na **de:** linha de uma mensagem de email. Esse valor é necessário.  
  
 
  
##  <a name="bkmk_use_configuration_manager"></a> Para configurar o email do servidor de relatório usando o Gerenciador de configuração do Reporting Services  
  
1.  Verifique se o serviço do Windows Servidor de Relatório tem permissões `Send As` no servidor SMTP.  
  
2.  Inicie o Gerenciador de Configurações do Reporting Services e conecte-se à instância do servidor de relatório.  
  
3.  Na página Configurações de Email, digite o nome do servidor SMTP. Esse valor pode ser um endereço IP, um nome UNC de um computador em sua intranet corporativa ou um nome de domínio totalmente qualificado.  
  
4.  Em **Endereço do Remetente**, digite o nome uma conta que tenha permissão para enviar email a partir do servidor SMTP.  
  
5.  Clique em **Aplicar**.  
  

  
##  <a name="bkmk_confiugre_remote_SMTP"></a> Para configurar um serviço SMTP remoto para o servidor de relatório  
  
1.  Verifique se o serviço do Windows Servidor de Relatório tem permissões `Send As` no servidor SMTP.  
  
2.  Abra o arquivo RSReportServer.config em um editor de texto.  
  
3.  Verifique <`UrlRoot`> é definido como o endereço de URL do servidor de relatório. Esse valor é definido quando você configura o servidor de relatório e já deveria estar preenchido. Se não estiver definido, digite o endereço da URL do servidor de relatório.  
  
4.  Na seção Entrega, localize <`ReportServerEmail`>.  
  
5.  Em <`SMTPServer`>, digite o nome do servidor SMTP. Esse valor pode ser um endereço IP, um nome UNC de um computador em sua intranet corporativa ou um nome de domínio totalmente qualificado.  
  
6.  Verifique se <`SendUsing`> está definido como 2. Se estiver definido como outro valor, o servidor de relatório não está configurado para usar um serviço SMTP remoto.  
  
7.  Em <`From`>, digite o nome de uma conta que tenha permissão para enviar email a partir do servidor SMTP.  
  
8.  Salve o arquivo.  
  
     O servidor de relatório usará as novas configurações automaticamente; você não precisa reiniciar o serviço. Você pode especificar configurações adicionais de SMTP para configurar mais como o servidor SMTP é usado para entrega de email do servidor de relatório. Para obter mais informações, consulte [Configurando um servidor de relatório para entrega de email](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  

  
##  <a name="bkmk_confiugre_local_SMTP"></a> Para configurar um serviço SMTP local para o servidor de relatório  
  
1.  No Painel de Controle, clique em **Adicionar ou Remover Programas**.  
  
2.  Clique em **Adicionar/Remover Componentes do Windows** para iniciar o Assistente de Componentes do Windows.  
  
3.  Selecione **Servidor de Aplicativos** e clique em **Detalhes**.  
  
4.  Selecione **Serviços de Informações da Internet (IIS)** e clique em **Detalhes**.  
  
5.  Marque a caixa de seleção **Serviço SMTP** e clique em **OK**.  
  
6.  No Assistente de Componentes do Windows, clique em **Avançar**. Clique em **Concluir**.  
  
7.  Verifique se o serviço está em execução no console **Serviços** .  
  
8.  Abra o arquivo **RSReportServer.config** em um editor de texto.  
  
9. Verifique se `<UrlRoot>` está configurado como o endereço da URL do servidor de relatório. Esse valor é definido quando você configura o servidor de relatório e já deveria estar preenchido. Se não estiver definido, digite o endereço da URL do servidor de relatório.  
  
10. Na seção Entrega, localize `<ReportServerEmail>.`  
  
11. Em `<SMTPServer>`, desmarque quaisquer valores para essa configuração, mas não exclua as marcas.  
  
12. Defina `<SendUsing>` como 1. Se estiver definido como outro valor, o servidor de relatório não está configurado para usar um serviço SMTP local.  
  
13. Defina `<SMTPServerPickupDirectory>` para uma pasta na unidade local.  
  
14. Configure `<From>` como uma conta que tenha permissão para enviar email a partir do servidor SMTP.  
  
15. Salve o arquivo.  
  
 
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
