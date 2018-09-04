---
title: Configurar a Autenticação do Windows no servidor de relatório | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [Reporting Services]
- Reporting Services, configuration
ms.assetid: 4de9c3dd-0ee7-49b3-88bb-209465ca9d86
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d111a77f80bf3d90fae14d23f68a301be731d366
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43268023"
---
# <a name="configure-windows-authentication-on-the-report-server"></a>Configurar a Autenticação do Windows no servidor de relatório
  Por padrão, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aceita solicitações que especificam a autenticação Negotiate ou NTLM. Se sua implantação incluir aplicativos cliente e navegadores que usam esses provedores de segurança, use os valores padrão sem nenhuma configuração adicional. Se desejar usar um provedor de segurança diferente para a segurança integrada do Windows (por exemplo, se desejar usar Kerberos diretamente) ou se tiver modificado os valores padrão e desejar restaurar as configurações originais, use as informações deste tópico para especificar configurações de autenticação no servidor de relatório.  
  
 Para usar a segurança integrada do Windows, cada usuário que precisa de acesso ao servidor de relatório deve ter uma conta de usuário de domínio ou local válida do Windows ou ser membro de uma conta de grupo de domínio ou local do Windows. Você pode incluir contas de outros domínios contanto que esses domínios sejam confiáveis. As contas devem ter acesso ao computador do servidor de relatório e devem ser atribuídas subsequencialmente às funções para obter acesso a operações específicas do servidor de relatório.  
  
 Os requisitos adicionais a seguir também devem ser satisfeitos:  
  
-   Os arquivos de configuração RSReportServer.config precisam ter **AuthenticationType** definido como **RSWindowsNegotiate**, **RSWindowsKerberos** ou **RSWindowsNTLM**. Por padrão, o arquivo RSReportServer.config incluirá a configuração **RSWindowsNegotiate** se a conta de serviço do Servidor de Relatórios for NetworkService ou LocalSystem; caso contrário, a definição **RSWindowsNTLM** será usada. Você poderá adicionar **RSWindowsKerberos** se tiver aplicativos que usam somente a autenticação Kerberos.  
  
    > [!IMPORTANT]  
    >  O uso de **RSWindowsNegotiate** resultará em um erro de autenticação se o serviço Servidor de Relatório for configurado para ser executado em uma conta de usuário de domínio e um SPN (nome da entidade de serviço) não tiver sido registrado para a conta. Para obter mais informações, consulte [Como resolver erros da autenticação Kerberos ao se conectar a um servidor de relatório](#proxyfirewallRSWindowsNegotiate) neste tópico.  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] deve ser configurado para a Autenticação do Windows. Por padrão, os arquivos Web.config do serviço Web Servidor de Relatórios incluem a configuração \<authentication mode="Windows">. Se você alterar essa configuração para \<authentication mode="Forms">, a Autenticação do Windows para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] falhará.  
  
-   Os arquivos Web.config do serviço Web Servidor de Relatórios devem ter \<identity impersonate= "true" />.  
  
-   O aplicativo cliente ou navegador deve dar suporte à segurança integrada do Windows.  

- O [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] não precisa de configuração adicional.
  
 Para alterar as configurações de autenticação do servidor de relatório, edite os elementos XML e os valores no arquivo RSReportServer.config. Você pode copiar e colar os exemplos deste tópico para implementar combinações específicas.  
  
 As configurações padrão funcionam melhor se todos os computadores cliente e de servidor estiverem no mesmo domínio ou em um domínio confiável e se o servidor de relatório for implantado para acessar a intranet por trás de um firewall corporativo. Os domínios únicos e confiáveis são um requisito para passar as credenciais do Windows. As credenciais poderão ser passadas mais de uma vez se você habilitar o protocolo Kerberos versão 5 para seus servidores. Caso contrário, elas podem ser passadas apenas uma vez antes de expirarem. Para obter mais informações sobre como configurar as credenciais para várias conexões de computador, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
 As instruções a seguir são válidas para um servidor de relatório no modo nativo. Se o servidor de relatório for implantado no modo integrado do SharePoint, use as configurações de autenticação padrão que especificam a segurança integrada do Windows. O servidor de relatório usa recursos internos na extensão padrão da Autenticação do Windows para dar suporte a servidores de relatório no modo integrado do SharePoint.  
  
## <a name="extended-protection-for-authentication"></a>Proteção Estendida para Autenticação  
 A partir do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o suporte para Proteção Estendida para Autenticação está disponível. O recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao uso de associação de canal e associação de serviço para aprimorar a proteção da autenticação. Os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precisam ser usados com um sistema operacional que ofereça suporte à Proteção Estendida. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] A configuração para proteção estendida é determinada pelas configurações no arquivo RSReportServer.config. O arquivo pode ser atualizado editando o arquivo ou usando APIs do WMI. Para obter mais informações, consulte [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
### <a name="to-configure-a-report-server-to-use-windows-integrated-security"></a>Para configurar um servidor de relatório para usar a segurança integrada do Windows  
  
1.  Abra o RSReportServer.config em um editor de texto.  
  
2.  Localize \<**Authentication**>.  
  
3.  Copie uma das estruturas XML a seguir que seja mais adequada para as suas necessidades. Você pode especificar **RSWindowsNegotiate**, **RSWindowsNTLM**e **RSWindowsKerberos** em qualquer ordem. Você deve habilitar a persistência de autenticação se desejar autenticar a conexão em vez de cada solicitação individual. Com a persistência de autenticação, todas as solicitações que precisam de autenticação serão permitidas durante a conexão.  
  
     A primeira estrutura XML será a configuração padrão quando a conta de serviço do Servidor de Relatório for NetworkService ou LocalSystem:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     A segunda estrutura XML será a configuração padrão quando a conta de serviço do Servidor de Relatório não for nem NetworkService nem LocalSystem:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    ```  
  
     \</Authentication>  
  
     A terceira estrutura XML especifica todos os pacotes de segurança usados na segurança integrada do Windows:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
                 <RSWindowsKerberos />  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
     A quarta estrutura XML especifica NTLM somente para implantações que não dão suporte a Kerberos ou como solução alternativa para erros de autenticação do Kerberos:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
4.  Cole-a nas entradas existentes de \<**Authentication**>.  
  
     Observe que você não pode usar **Personalizado** com os tipos **RSWindows** .  
  
5.  Modifique as configurações para proteção estendida conforme o necessário. A proteção estendida é desabilitada por padrão.  Se estas entradas não estiverem presentes, o computador atual poderá não estar executando uma versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que dá suporte à proteção estendida. Para obter mais informações, consulte [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
    ```  
          <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
    ```  
  
6.  Salve o arquivo.  
  
7.  Se você configurou uma implantação em expansão, repita essas etapas para outros servidores de relatório na implantação.  
  
8.  Reinicie o servidor de relatório para terminar as sessões que estão atualmente abertas.  
  
##  <a name="proxyfirewallRSWindowsNegotiate"></a> Resolving Kerberos Authentication Errors When Connecting to a Report Server  
 Em um servidor de relatório configurado para a autenticação Negotiate ou Kerberos, uma conexão cliente com o servidor de relatório falhará se houver um erro da autenticação Kerberos. Os erros da autenticação Kerberos normalmente ocorrem quando:  
  
-   O serviço Servidor de Relatório é executado como uma conta de usuário de domínio do Windows e um nome da entidade de serviço (SPN) não tiver sido registrado para a conta.  
  
-   O servidor de relatório está configurado com a definição **RSWindowsNegotiate** .  
  
-   O navegador escolhe Kerberos em vez de NTLM no cabeçalho de autenticação na solicitação que envia ao servidor de relatório.  
  
 Você pode detectar o erro se tiver habilitado o log de Kerberos. Outro sintoma do erro é a solicitação das credenciais várias vezes e a exibição de uma janela vazia do navegador.  
  
 Você pode confirmar que está tendo um erro de autenticação Kerberos removendo < **RSWindowsNegotiate** /> do arquivo de configuração e tentando estabelecer a conexão novamente.  
  
 Depois que você confirmar o problema, poderá solucioná-lo dos seguintes modos:  
  
-   Registre um SPN para o serviço Servidor de Relatório na conta do usuário de domínio. Para obter mais informações, consulte [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
-   Altere a conta de serviço para ser executada em uma conta interna, como Serviço de Rede. As contas internas mapeiam o SPN HTTP ao SPN do host, o qual é definido quando um computador se une à sua rede. Para obter mais informações, consulte [Configurar uma conta de serviço &#40; 	Gerenciador de Configurações do SSRS&#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0).  
  
-   Use NTLM. O NTLM geralmente funciona quando a autenticação Kerberos falha. Para usar NTLM, remova **RSWindowsNegotiate** do arquivo RSReportServer.config e verifique se somente **RSWindowsNTLM** está especificado. Se você optar por essa abordagem, poderá continuar usando uma conta de usuário de domínio para o serviço Servidor de Relatório, mesmo que não haja um SPN definido.  
  
#### <a name="logging-information"></a>Registrando informações  
 Há várias fontes de registros de informações que podem ajudar a resolver problemas relacionados ao Kerberos.  
  
##### <a name="user-account-control-attribute"></a>Atributo de controle da conta de usuário  
 Determine se a conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tem o atributo suficiente definido no Active Directory. Revise o arquivo de log de rastreamento do serviço de relatório para localizar o valor registrado em log para o atributo UserAccountControl. O valor registrado em log está em decimais. Você precisa converter o valor decimal para a forma hexadecimal e, em seguida, localizar o valor no tópico do MSDN que descreve o atributo de controle da conta de usuário.  
  
-   A entrada do log de rastreamento do serviço de relatório será semelhante ao seguinte:  
  
    ```  
    appdomainmanager!DefaultDomain!8f8!01/14/2010-14:42:28:: i INFO: The UserAccountControl value for the service account is 590336  
    ```  
  
-   Uma opção para converter o valor decimal para a forma hexadecimal é, para nós, a Calculadora do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. A Calculadora do Windows oferece suporte a vários modos que mostram as opções 'Dec' e 'Hex'. Selecione a opção 'Dec', cole ou digite no valor decimal encontrado no arquivo de log e, em seguida, selecione a opção 'Hex'.  
  
-   Em seguida, consulte o tópico [Atributo de controle da conta de usuário](http://go.microsoft.com/fwlink/?LinkId=183366) para derivar o atributo para a conta de serviço.  
  
##### <a name="spns-configured-in-active-directory-for-the-reporting-services-service-account"></a>Os SPNs configurados no Active Directory para a conta de serviço do Reporting Services.  
 Para registrar os SPNs no arquivo de log de rastreamento de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você pode habilitar o recurso de Proteção Estendida do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] temporariamente.  
  
-   Modifique o arquivo de configuração **rsreportserver.config** definindo o seguinte:  
  
    ```  
    <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>   
    <RSWindowsExtendedProtectionScenario>Any</RSWindowsExtendedProtectionScenario>  
    ```  
  
-   Reinicie o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e procure entradas semelhantes às seguintes no arquivo de log de rastreamento:  
  
    ```  
    rshost!rshost!e44!01/14/2010-14:43:51:: i INFO: Registered valid SPNs list for endpoint 2: rshost!rshost!e44!01/14/2010-14:43:52:: i INFO: SPN Whitelist Added <Explicit> - \<HTTP/sqlpod064-13.w2k3.net>.  
    ```  
  
-   Os valores em \<Explicit> conterão os SPNs configurados no Active Directory para a conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Se você não desejar continuar usando a Proteção Estendida, defina os valores de configuração para os padrões e reinicie a conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
```  
<RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>  
<RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
```  
  
 Para obter mais informações, consulte [Proteção estendida para autenticação com o Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
#### <a name="how-the-browser-chooses-negotiated-kerberos-or-negotiated-ntlm"></a>Como o navegador escolhe Kerberos negociado ou NTLM negociado  
 Quando você usa o Internet Explorer para se conectar ao servidor de relatório, Kerberos negociado ou NTLM negociado é especificado no cabeçalho de autenticação. NTLM é usado em vez de Kerberos quando:  
  
-   A solicitação é enviada a um servidor de relatório local.  
  
-   A solicitação é enviada a um endereço IP do computador do servidor de relatório em vez de um cabeçalho host ou nome de servidor.  
  
-   O software do firewall bloqueia as portas usadas para autenticação Kerberos.  
  
-   O sistema operacional de um servidor específico não tem Kerberos habilitado.  
  
-   O domínio inclui versões mais antigas dos sistemas operacionais de cliente e servidor do Windows que não dão suporte ao recurso da autenticação Kerberos incorporado nas versões mais recentes do sistema operacional.  
  
 Além disso, o Internet Explorer pode optar entre Kerberos ou NTLM negociado dependendo da configuração de URL, LAN e proxy.  
  
###### <a name="report-server-url"></a>URL do servidor de relatório  
 Se o URL incluir um nome de domínio completamente qualificado, o Internet Explorer selecionará NTLM. Se o URL especificar localhost, o Internet Explorer selecionará NTLM. Se o URL especificar o nome de rede do computador, o Internet Explorer selecionará Negotiate, que será bem-sucedido ou falhará dependendo da existência de um SPN para a conta de serviço do Servidor de Relatório.  
  
###### <a name="lan-and-proxy-settings-on-the-client"></a>Configurações de LAN e proxy no cliente  
 As configurações de LAN e proxy que você definiu no Internet Explorer podem determinar a escolha de NTLM em vez de Kerberos. No entanto, como as configurações de LAN e proxy varia entre as organizações, não é possível determinar as configurações exatas que contribuem para os erros da autenticação Kerberos. Por exemplo, sua organização pode impor configurações de proxy que convertem URLs de intranet em URLs de nome completo de domínio resolvidas nas conexões da Internet. Se diferentes provedores de autenticação forem usados para diferentes tipos de URL, algumas conexões podem ser bem-sucedidas e outras podem falhar.  
  
 Se houver erros de conexão que, na sua opinião, ocorreram devido a falhas de autenticação, tente usar combinações diferentes de configurações de LAN e proxy para isolar o problema. No Internet Explorer, as configurações de LAN e proxy estão disponíveis na caixa de diálogo **Configurações de Rede Local (LAN)** , que é exibida ao clicar em **Configurações de LAN** na guia **Conexão** de **Opções da Internet**.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Para obter informações adicionais referentes ao Kerberos e a servidores de relatórios, consulte [Deploying a Business Intelligence Solution Using SharePoint, Reporting Services, and PerformancePoint Monitoring Server with Kerberos](http://go.microsoft.com/fwlink/?LinkID=177751)(em inglês).  
  
## <a name="see-also"></a>Consulte Também  
 [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Configurar a autenticação Básica no servidor de relatório](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
 [Configurar a autenticação personalizada ou de formulários no servidor de relatório](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)   
 [Proteção estendida para autenticação com o Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  
