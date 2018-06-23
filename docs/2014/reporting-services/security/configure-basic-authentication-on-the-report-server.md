---
title: Configurar a autenticação Básica no servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
caps.latest.revision: 25
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 2611f683ee02180bc5b90b0b08fe961d049e9aab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120071"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>Configurar autenticação básica no Servidor de Relatório
  Por padrão, o Reporting Services aceita solicitações que especificam a autenticação Negotiate e NTLM. Se a sua implantação inclui aplicativos cliente ou navegadores que usam autenticação Básica, adicione a autenticação Básica à lista de tipos suportados. Além disso, para usar o Construtor de Relatórios, você deve habilitar o acesso Anônimo aos arquivos do Construtor de Relatórios.  
  
 Para configurar a autenticação Básica no servidor de relatório, edite os elementos XML e os valores no arquivo RSReportServer.config. É possível copiar e colar os exemplos deste tópico para substituir os valores padrão.  
  
 Antes de habilitar a autenticação Básica, verifique se a sua infraestrutura de segurança dá suporte a ela. Na autenticação Básica, o serviço Web Servidor de Relatórios passará credenciais para a autoridade de segurança local. Se as credenciais especificarem uma conta de usuário local, o usuário será autenticado pela autoridade de segurança local no computador do servidor de relatório e o usuário obterá um token de segurança válido para recursos locais. As credenciais de contas de usuário de domínio são encaminhadas para um controlador de domínio e autenticadas por ele. A permissão resultante é válida para recursos de rede.  
  
 A criptografia de canal, como SSL, será necessária se você quiser minimizar o risco de as credenciais serem interceptadas durante o envio para um controlador de domínio da sua rede. Por si só, autenticação Básica transmite o nome do usuário em texto não criptografado e a senha na codificação em base 64. Quando adicionada, a criptografia de canal torna o pacote ilegível. Para obter mais informações, veja [Configurar conexões SSL em um Servidor de Relatórios do Modo Nativo](configure-ssl-connections-on-a-native-mode-report-server.md).  
  
 Depois de habilitar a autenticação Básica, lembre-se que os usuários não podem selecionar a opção **Segurança integrada do Windows** ao definir as propriedades de conexão para uma fonte de dados externa que forneça dados a um relatório. A opção ficará indisponível nas páginas de propriedades da fonte de dados.  
  
> [!NOTE]  
>  As instruções a seguir são válidas para um servidor de relatório no modo nativo. Se o servidor de relatório for implantado no modo integrado do SharePoint, use as configurações de autenticação padrão que especificam a segurança integrada do Windows. O servidor de relatório usa recursos internos da extensão padrão da Autenticação do Windows para dar suporte ao servidor de relatório no modo integrado do SharePoint.  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>Para configurar um servidor de relatório para usar a autenticação Básica  
  
1.  Abra o RSReportServer.config em um editor de texto.  
  
     O arquivo está localizado em  *\<unidade >:* \Program Files\Microsoft SQL msrs12. MSSQLSERVER\Reporting Services\ReportServer.  
  
2.  Localizar <`Authentication`>.  
  
3.  Copie uma das estruturas XML a seguir que seja mais adequada para as suas necessidades. A primeira estrutura XML oferece espaços reservados para especificar todos os elementos, que estão descritos na próxima seção:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     Se você estiver usando valores padrão, poderá copiar a estrutura de elementos mínima:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  Cole-o sobre entradas existentes para <`Authentication`>.  
  
     Se você estiver usando vários tipos de autenticação, adicione apenas o `RSWindowsBasic` elemento, mas não exclua as entradas para `RSWindowsNegotiate`, `RSWindowsNTLM`, ou `RSWindowsKerberos`.  
  
     Para fins de compatibilidade com o navegador Safari, não é possível configurar o servidor de relatório para usar diversos tipos de autenticação. Você deve especificar somente `RSWindowsBasic` e excluir as outras entradas.  
  
     Observe que não é possível usar `Custom` com outros tipos de autenticação.  
  
5.  Substitua valores vazios de <`Realm`> ou <`DefaultDomain`> por valores válidos para seu ambiente.  
  
6.  Salve o arquivo.  
  
7.  Se você configurou uma implantação em expansão, repita essas etapas para outros servidores de relatório na implantação.  
  
8.  Reinicie o servidor de relatório para terminar as sessões que estão atualmente abertas.  
  
## <a name="rswindowsbasic-reference"></a>Referência de RSWindowsBasic  
 Os elementos a seguir podem ser especificados na configuração da autenticação Básica.  
  
|Elemento|Obrigatório|Valores válidos|  
|-------------|--------------|------------------|  
|LogonMethod|Sim<br /><br /> Se você não especificar um valor, será usado 3.|`2` = Logon de rede, indicado para servidores de alto desempenho autenticar senhas de texto sem formatação.<br /><br /> `3` = Logon de texto não criptografado, que preserva as credenciais de logon no pacote de autenticação é enviada com cada solicitação HTTP, permitindo que o servidor representar o usuário ao se conectar a outros servidores na rede. (Padrão)<br /><br /> Observação: valores 0 (para logon interativo) e 1 (para logon em lotes) não têm suporte no [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|Realm|Opcional|Especifica uma partição de recursos que inclui recursos de autorização e autenticação usados para controlar o acesso a recursos protegidos da organização.|  
|DefaultDomain|Opcional|Especifica o domínio usado pelo servidor para autenticar o usuário. Este valor é opcional, mas, caso seja omitido, o servidor de relatório usará o nome do computador como domínio. Se o computador for um membro de domínio, esse domínio será o padrão. Se você instalou o servidor de relatório em um controlador de domínio, o domínio usado será o que é controlado pelo computador.|  
  
## <a name="enabling-anonymous-access-to-report-builder-application-files"></a>Habilitando o acesso Anônimo para arquivos do aplicativo Construtor de Relatórios  
 O Construtor de Relatórios usa a tecnologia ClickOnce para baixar e instalar arquivos de aplicativo no computador cliente. Quando ele é iniciado no computador cliente, o iniciador do aplicativo ClickOnce solicita arquivos de aplicativo adicionais no computador do servidor de relatório. Se o servidor de relatório estiver configurado para autenticação Básica, o iniciador do aplicativo ClickOnce não passará na verificação da autenticação porque não dá suporte à autenticação Básica.  
  
 Para contornar esse problema, você pode configurar o acesso Anônimo para arquivos de programa do Construtor de Relatórios. Dessa forma, a tecnologia ClickOnce ignorará a verificação de autenticação quando recuperar seus arquivos. Para habilitar o acesso Anônimo, faça o seguinte:  
  
-   Verifique se o servidor de relatório está configurado para autenticação Básica.  
  
-   Crie uma pasta bin em ReportBuilder e copie quatro assemblies para ela.  
  
-   Acrescente o elemento `IsReportBuilderAnonymousAccessEnabled` ao arquivo RSReportServer.config e defina-o como `True`. Depois que você salvar o arquivo, o servidor de relatório criará um novo ponto de extremidade para o Construtor de Relatórios. O ponto de extremidade é usado internamente para acessar arquivos de programa e não tem uma interface programática que possa ser usada em código. Quando há um ponto de extremidade separado, o Construtor de Relatórios pode ser executado em seu próprio domínio de aplicativo dentro do limite de processo do serviço Servidor de Relatório.  
  
-   Se preferir, você poderá especificar uma conta com menos privilégios para processar solicitações em um contexto de segurança diferente do servidor de relatório. Essa conta passa a ser a conta anônima que dá acesso a arquivos do Construtor de Relatórios em um servidor de relatório. A conta define a identidade do thread no processo de trabalho do ASP.NET. As solicitações executadas nesse thread são passadas para o servidor de relatório sem uma verificação de autenticação. Essa conta é equivalente a conta IUSR _\<máquina > conta no Internet Information Services (IIS), que é usado para definir o contexto de segurança para ASP.NET trabalho processa quando o acesso anônimo e representação estão habilitados. Para especificar a conta, adicione-a a um arquivo Web.config do Construtor de Relatórios.  
  
 O servidor de relatório deve ser configurado para autenticação Básica se você quiser habilitar o acesso Anônimo para os arquivos de programa do Construtor de Relatórios. Se o servidor de relatório não estiver configurado para a autenticação Básica, você receberá um erro quando tentar habilitar o acesso Anônimo.  
  
 Para obter mais informações sobre problemas de autenticação e o Construtor de Relatórios, consulte [Configurar o acesso do Construtor de Relatórios](../report-server/configure-report-builder-access.md).  
  
#### <a name="to-configure-report-builder-access-on-a-report-server-configured-for-basic-authentication"></a>Para configurar o acesso do Construtor de Relatórios em um servidor de relatório configurado para autenticação Básica  
  
1.  Verifique nas configurações de autenticação do arquivo RSReportServer.config se o servidor de relatório está configurado para autenticação Básica.  
  
2.  Crie uma pasta BIN sob a pasta ReportBuilder. Por padrão, essa pasta está localizada em \Arquivos de Programas\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\ReportBuilder.  
  
3.  Copie os seguintes assemblies da pasta ReportServer\Bin para a pasta ReportBuilder\BIN:  
  
     Microsoft.ReportingServices.Diagnostics.dll  
  
     Microsoft.ReportingServices.Interfaces.dll  
  
     ReportingServicesAppDomainManager.dll  
  
     RSHttpRuntime.dll  
  
4.  Opcionalmente, crie um arquivo Web.config para processar solicitações do Construtor de Relatórios com uma conta Anônima:  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
    <system.web>  
    <authentication mode="Windows" />    
    <identity impersonate="true " userName="username" password="password"/>  
    </system.web>  
    </configuration>  
    ```  
  
     Modo de autenticação deve ser definido como `Windows` se você incluir um arquivo Web. config.  
  
     `Identity impersonate` pode ser `True` ou `False`.  
  
    -   Defina-a como `False` se você não deseja que o ASP.NET leia o token de segurança. A solicitação será executada no contexto de segurança do serviço Servidor de Relatórios.  
  
    -   Defina-a como `True` se você deseja que o ASP.NET leia o token de segurança de camada do host. Se você defini-lo como `True`, também deverá especificar `userName` e `password` para designar uma conta Anônima. As credenciais especificadas determinarão o contexto de segurança sob o qual a solicitação é emitida.  
  
5.  Salve o arquivo Web.config na pasta ReportBuilder\bin.  
  
6.  Localizar o arquivo rsreportserver. config aberto, na seção serviços, `IsReportManagerEnabled` e adicione a seguinte configuração abaixo dele:  
  
    ```  
    <IsReportBuilderAnonymousAccessEnabled>True</IsReportBuilderAnonymousAccessEnabled>  
    ```  
  
7.  Salve RSReportServer.config e feche o arquivo.  
  
8.  Reinicie o servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Domínios de aplicativo para aplicativos de servidor de relatório](../report-server/application-domains-for-report-server-applications.md)   
 [Segurança e proteção do Reporting Services](reporting-services-security-and-protection.md)  
  
  