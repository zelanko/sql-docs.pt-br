---
title: "Solucionar problemas de uma instalação do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 79d064c7ddb43531fdff086eda71ba1e28d71fd6
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="troubleshoot-a-reporting-services-installation"></a>Solucionar um problema da instalação do Reporting Services

  Se você não puder instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devido a erros ocorridos durante a Instalação, use as instruções deste tópico para identificar as condições mais prováveis que causam erros de instalação.  
  
 Para obter informações sobre outros erros e problemas relacionados ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte [Solução de problemas e erros do SSRS.](http://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx)  
  
 Revise as [Notas de versão online](http://go.microsoft.com/fwlink/?linkid=236893) caso o problema que você encontrar seja descrito nas notas de versão.  
  
##  <a name="bkmk_setuplogs"></a> Verificar logs de instalação  
 Os erros de instalação são registrados em arquivos de log na pasta **[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Setup Bootstrap\Log** . Uma subpasta é criada toda vez que você executa a Instalação. O nome da subpasta é a hora e a data em que você executou a Instalação. Para obter instruções sobre como exibir os arquivos de log da Instalação, veja [Exibir e ler os arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
-   Os arquivos de log incluem uma coleção de arquivos.  
  
-   Abra o arquivo * _summary.txt para exibir informações sobre o produto, o componente e a instância.  
  
-   Abra o arquivo * _errorlog.txt para exibir informações de erro geradas durante a Instalação.  
  
-   Abra o arquivo *_RS\_\*_ComponentUpdateSetup.log para ver informações da instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
##  <a name="bkmk_prereq"></a> Verificar pré-requisitos  
 A Instalação verifica os pré-requisitos automaticamente. Entretanto, se você estiver solucionando problemas de instalação, será útil saber quais requisitos a Instalação está verificando.  
  
-   Os requisitos de conta para executar a Instalação inclui associação no grupo Administradores local. A Instalação deve ter permissão para adicionar arquivos, configurações de registro, criar grupos de segurança locais e definir permissões. Se você estiver instalando uma configuração padrão, a instalação deverá ter permissão para criar um banco de dados de servidor de relatório na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que será feita a instalação.  
  
-   O Sistema Operacional deve dar suporte a HTTP.SYS 1.1.  
  
-   O serviço HTTP deve estar habilitado e em execução.  
  
-   O DTC (Coordenador de Transações Distribuídas) deve estar em execução se você também estiver instalando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   Authz.dll deve estar presente na pasta System32.  
  
 A instalação não verifica mais Serviços de Informações da Internet (IIS) nem [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]requer o MDAC 2.0 e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] versão 2.0; A instalação instalará esses se eles não ainda estiverem instalados.  
  
##  <a name="bkmk_tshoot_sharepoint"></a> Solucionar problemas com instalações do modo do SharePoint  
  
-   [O Gerenciador de Configuração do Reporting Services não inicia](#bkmk_configmanager_notstart)  
  
-   [O serviço do SQL Server Reporting Services não é exibido na Administração Central do SharePoint após a instalação do SQL Server 2016 SSRS no modo do SharePoint](#bkmk_no_ssrs_service)  
  
-   [Os cmdlets do PowerShell do Reporting Services não estão disponíveis e os comandos não são reconhecidos](#bkmk_cmdlets_not_recognized)  
  
-   [Você vê uma mensagem de erro indicando que a URL não está configurada](#bkmk_URL_not_configured)  
  
-   [A Instalação falha quando é realizada em um computador com o SharePoint instalado, mas não configurado](#bkmk_sharepoint_not_confiugred)  
  
-   [A página Administração Central do SharePoint está vazia](#bkmk_central_admin_blank)  
  
-   [Você vê uma mensagem de erro quando tenta criar um novo relatório do Construtor de Relatórios](#bkmk_reportbuilder_newreport_error)  
  
-   [Você vê uma mensagem de erro informando que RS_SHP não tem suporte com o PREPAREIMAGE](#bkmk_RS_SHP_notsupported)  

### <a name="bkmk_configmanager_notstart"></a> O Gerenciador de Configuração do Reporting Services não inicia

 **Descrição:** esse problema ocorre por design no SQL Server 2012 e versões posteriores. O Reporting Services foi projetado para a arquitetura de serviço do SharePoint. O Gerenciador de Configuração não é mais necessário para configurar e administrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo SharePoint.  
  
 **Solução alternativa:** Use a Administração Central do SharePoint para configurar um servidor de relatório no modo do SharePoint. Para obter mais informações, veja [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_no_ssrs_service"></a>Você não vir o serviço SQL Server Reporting Services na Administração Central do SharePoint após a instalação do SQL Server 2016 SSRS no modo do SharePoint  
 **Descrição:** se depois de instalar com êxito o SQL Server 2016 Reporting Services no modo do SharePoint e o SQL Server 2016 Reporting Services suplemento para SharePoint 2013/2016, você não vir "SQL Server Reporting Services" nos dois menus a seguir, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço não foi registrado:  
  
-   Página Administração Central do SharePoint 2013/2016 -> “Gerenciamento de Aplicativo” -> “Gerenciar Serviços no Servidor”  
  
-   Administração Central do SharePoint 2013/2016 -> “Gerenciamento de Aplicativo” -> “Gerenciar aplicativos de serviço” ->Menu “Novo”  
  
 **Solução alternativa:** Para registrar e iniciar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Services, conclua o seguinte:  
  
1.  No computador que executa a Administração Central do SharePoint 2013/2016  
  
    1.  Abra o Shell de Gerenciamento do SharePoint 2013/2016 com privilégios de administrador. Clique com o botão direito no ícone e clique em "Executar como administrador". Execute os três cmdlets a seguir do shell:  
  
    2.  ```  
        Install-SPRSService  
        ```  
  
    3.  ```  
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```  
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  Verifique se o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço mostra o status como "**iniciado**" na página: Administração Central do SharePoint 2013/2016-> "**gerenciamento de aplicativos**"->"**gerenciar serviços no servidor**"  
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_cmdlets_not_recognized"></a> Os cmdlets do PowerShell do Reporting Services não estão disponíveis e os comandos não são reconhecidos  
 **Descrição:** ao tentar executar um cmdlet do PowerShell do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você receberá uma mensagem de erro semelhante à seguinte:  
  
-   O termo 'Install-SPRSServiceInstall-SPRSService' **não é reconhecido** como nome de um cmdlet, função, arquivo de script ou programa operável. Verifique a ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está correto e tente novamente.At line:1 char:39+ Install-SPRSServiceInstall-SPRSService <<<<    + CategoryInfo          : ObjectNotFound: (Install-SPRSServiceInstall-SPRSService:String) [], CommandNotFoundExcep  
  
 **Solução alternativa:** Concluir um dos seguintes:  
  
-   Execute o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint. **rssharepoint.msi**.  
  
-   Instale o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da mídia de instalação do SQL Server.  
  
 **Observação:** se o **Shell de Gerenciamento do SharePoint 2013/2016** estiver aberto quando você concluir uma das soluções alternativas, feche e reabra o shell de gerenciamento.  
  
 Para obter mais informações, consulte o seguinte:  
  
-   [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Instalar o Primeiro Servidor de Relatório no Modo do SharePoint](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538)  
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_URL_not_configured"></a> Você vê uma mensagem de erro indicando que a URL não está configurada  
 **Descrição:** você vê uma mensagem de erro semelhante à seguinte:  
  
 Essa funcionalidade do SSRS (SQL Server Reporting Services) não tem suporte. Use a Administração Central para verificar e corrigir um ou mais dos seguintes problemas:
 
 - Uma URL do servidor de relatório não está configurada. Use a página de Integração do SSRS para defini-la.
 
 - O proxy de aplicativo de serviço do SSRS não está configurado. Use as páginas de aplicativo de serviço do SSRS para configurar o proxy.
 
 - O aplicativo de serviço do SSRS não está mapeado para este aplicativo Web. Use as páginas do aplicativo de serviço do SSRS para associar o proxy do aplicativo de serviço SSRS ao Grupo Proxy de Aplicativo para esse aplicativo web. 
  
 **Solução alternativa:** A mensagem de erro contém três etapas sugeridas para corrigir este problema. A primeira sugestão na mensagem 'Um URL do servidor de relatório não está configurado...' é relevante ao integrar a versão do servidor de relatório anterior para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. A Configuração do SharePoint para as versões de servidor de relatório anteriores é concluída na página **Configurações Gerais do Aplicativo** , usando **SQL Server Reporting Services (2008 e 2008 R2)**.  
  
 **Mais informações:** Você verá esta mensagem de erro ao tentar usar qualquer funcionalidade do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que exige uma conexão com o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Isso inclui:  
  
-   Abrindo o Construtor de Relatórios do SQL Server de uma biblioteca de documentos do SharePoint.  
  
-   Gerenciar assinaturas.  
  
-   Gerenciar um aplicativo de serviço.  
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_sharepoint_not_confiugred"></a> A Instalação falha quando é realizada em um computador com o SharePoint instalado, mas não configurado  
 **Descrição:** se você optar por instalar o modo do SharePoint do Reporting Services em um computador que tenha o SharePoint instalado, mas não configurado, verá uma mensagem semelhante à seguinte, e a instalação será interrompida:  
  
 A Instalação do SQL Server parou de funcionar  
  
 **Solução alternativa:** Configure o SharePoint e execute a instalação do SQL Server.  
  
 **Mais informações:** Ao instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma instalação do SharePoint existente, a instalação tenta instalar e inicia o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint. Se o SharePoint não estiver configurado, ocorrerá falha na instalação do serviço, e a instalação não será concluída.  
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_central_admin_blank"></a> A página Administração Central do SharePoint está vazia  
 **Descrição:** você conseguiu instalar o SharePoint 2013/2016 com êxito, sem erros de instalação. No entanto, quando você navega até a Administração Central, vê somente uma página em branco:  
  
 **Solução alternativa:** Este problema não é específico do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , mas está relacionado com a configuração de permissões na instalação geral do SharePoint. Esta é uma lista de sugestões:  
  
-   Examine o tópico do SharePoint sobre ambientes de desenvolvimento. [Configurar um ambiente de desenvolvimento geral para o SharePoint](https://msdn.microsoft.com/library/ee554869)  
  
-   Examine a publicação do fórum: [Administração Central retorna página em branco depois da instalação no Windows 7](http://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)  
  
-   A conta Serviço que você está usando para serviços do SharePoint como o Serviço de Administração Central do SharePoint 2013/2016 deve ter privilégios administrativos no sistema operacional local.  
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_reportbuilder_newreport_error"></a> Você vê uma mensagem de erro quando tenta criar um novo relatório do Construtor de Relatórios  
 **Descrição:** você vê uma mensagem de erro semelhante à seguinte quando tenta criar um relatório do Construtor de Relatórios dentro de uma biblioteca de documentos:  
  
 Essa funcionalidade não tem suporte porque o aplicativo de serviço do SQL Server Reporting Services não existe ou uma URL do servidor de relatórios não foi configurada na Administração Central.  
  
 **Solução alternativa:** Verifique se você tem um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e se ele foi configurado corretamente. Para obter mais informações, veja [Instalar o Primeiro Servidor de Relatório no Modo do SharePoint](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_RS_SHP_notsupported"></a> Você vê uma mensagem de erro informando que RS_SHP não tem suporte com o PREPAREIMAGE  
 **Descrição:** Ao tentar executar PREPAREIMAGE para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você recebe uma mensagem de erro semelhante à seguinte:  
  
 "O recurso 'RS_SHP' especificado não tem suporte ao executar a ação PREPAREIMAGE, porque ele não dá suporte a SysPrep. Remova os recursos que não são compatíveis com SysPrep e execute a instalação novamente."  
  
 **Solução alternativa:** Não existe solução. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte a SYSPREP (PREPAREIMAGE). [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Native oferece suporte a SYSPREP.  
  
 ![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
##  <a name="bkmk_tshoot_native"></a> Solucionar problemas com instalações do modo Nativo  
  
###  <a name="PerfCounters"></a> Os contadores de desempenho não ficam visíveis após atualização para o Windows Vista ou Windows Server 2008  
 Se você atualizar o sistema operacional para [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] ou [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] em um computador que executa o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], os contadores de desempenho do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não serão definidos após a atualização.  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>Para instanciar novamente os contadores de desempenho do Reporting Services  
  
1.  Exclua as seguintes chaves do Registro:  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service**  
  
2.  Abra uma janela de comando e digite o seguinte comando no prompt:  
  
    -   **executar \<**  *.NET 4.0 Framework directory* **> \InstallUtil.exe \< ** *Report Server Bin directory* **> \ReportingServicesLibrary.dll**  
  
        > [!NOTE]  
        >  Substituir \< *.NET 4.0 Framework directory*> pelo caminho físico do .NET Framework 4.0 arquivos e \< *Report Server Bin directory*> pelo caminho físico dos arquivos binários do servidor de relatório.  
  
3.  Reinicie o serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para verificar se as etapas funcionam, abra um navegador da Web e navegue até o portal da web, URL ou a URL do servidor de relatório. Abra o Monitor de Desempenho para verificar se os contadores estão funcionando.  
  
#### <a name="to-re-add-the-performance-registry-keys-by-using-registry-editor"></a>Para adicionar novamente as chaves de Registro de desempenho usando o Editor do Registro  
  
1.  Abra o Editor do Registro:  
  
    1.  Clique em **Iniciar**e em **Executar**.  
  
    2.  Na caixa de diálogo **Executar** , na caixa **Abrir** , digite **regedit**.  
  
2.  No Editor do Registro, selecione a seguinte chave: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
3.  Clique com o botão direito do mouse no nó **Desempenho** , aponte para **Novo**e clique em **Valor com Várias Cadeias de Caracteres**.  
  
4.  Digite **Counter Names** e pressione ENTER.  
  
5.  Repita para adicionar a chave de registro **Counter Types** nesse nó.  
  
6.  Navegue até esta chave de Registro: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
7.  Clique com o botão direito do mouse no nó **Desempenho** , aponte para **Novo**e clique em **Valor com Várias Cadeias de Caracteres**.  
  
8.  Digite **Counter Names** e pressione ENTER.  
  
9. Repita para adicionar a chave de registro **Counter Types** nesse nó.  
  
 Depois que reparar a instância de 64 bits ou adicionar as chaves de Registro manualmente de novo, você poderá usar o Monitor de Desempenho para configurar os objetos de desempenho do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que deseja monitorar.  
  
###  <a name="ConfigPropsMissing"></a> As propriedades de configuração ReportServerExternalURL e PassThroughCookies não são configuradas após uma atualização do SQL Server 2005  
 Quando você atualiza do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], as propriedades de configuração de **ReportServerExternalURL** e **PassThroughCookies** não são configuradas pelo processo de atualização. **ReportServerExternalURL** é uma propriedade opcional e deve ser definida se você estiver usando o SharePoint 2.0 Web Parts e deseja que os usuários possam recuperar um relatório e abri-lo em uma nova janela do navegador. Para obter mais informações sobre **ReportServerExternalURL**, consulte [URLs em arquivos de configuração &#40; Gerenciador de configurações do SSRS &#41; ](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md). **PassThroughCookies** só é necessário ao usar o método de autenticação Personalizado. Para obter mais informações sobre **PassThroughCookies**, consulte [configurar o Portal da Web para transmitir Cookies de autenticação personalizados](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).  
  
> [!NOTE]  
>  Quando você usar a autenticação Personalizada, será recomendável migrar a instalação, em vez de executar uma atualização. Para obter mais informações sobre como migrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [migrar uma instalação do Reporting Services &#40; Modo nativo &#41; ](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 Por padrão, essas propriedades não existem na configuração do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Caso você tenha configurado essas propriedades no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e continuar exigindo a funcionalidade fornecida por elas, adicione-as manualmente ao arquivo **RSReportServer.config** após o processo de atualização. Para obter mais informações, consulte [modificar um arquivo de configuração do Reporting Services &#40; Rsreportserver. config &#41; ](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  

### <a name="WindowsAuthBreaksAfterUpgrade"></a>Erro 401-não autorizado ao usar a autenticação do Windows após uma atualização do SQL Server 2005 para SQL Server 2016

 Se você atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]e usar a autenticação NTLM com uma conta interna para a conta de serviço do servidor de relatório, você pode encontrar um erro 401-não autorizado ao acessar o servidor de relatório ou o portal da web após a atualização.  
  
 Isso ocorre devido a uma alteração na configuração padrão do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para autenticação do Windows. A negociação é configurada quando a conta do serviço Servidor de Relatórios é Serviço de Rede ou Sistema Local. O NTLM é configurado quando a conta do serviço Servidor de Relatórios não é uma dessas contas internas. Para corrigir o problema após atualizar, você pode editar o arquivo RSReportServer.config e configurar **AuthenticationType** para ser **RSWindowsNTLM**. Para obter mais informações, consulte [Configure Windows Authentication on the Report Server](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).  

### <a name="Uninstall32BitBreaks64Bit"></a>Desinstalar a instância de 32 bits do SQL Server 2016 Reporting Services na implantação lado a lado com uma instância de quebras de 64 bits da instância de 64 bits

 Quando você instala uma instância de 32 bits e uma instância de 64 bits do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] lado a lado em um computador, e desinstalar a instância de 32 bits, quatro chaves do Registro do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são removidas. Isso trava a instância de 64 bits do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. As chaves do Registro do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que são removidas quando você desinstala a instância de 32 bits são:  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Types`  
  
 Para corrigir o problema, repare a instância de 64 bits. Embora seja recomendável usar o reparo, você pode adicionar outra vez as chaves do Registro manualmente usando o Editor do Registro.  
  
> [!CAUTION]  
>  A edição incorreta do Registro pode danificar seriamente o sistema. Antes de alterar o Registro, faça um backup dos dados importantes do computador.  
  
##  <a name="bkmk_additional"></a> Recursos adicionais  
 A seguir, veja os recursos adicionais que você pode examinar para auxiliá-lo com solução de problemas:  
  
-   Wiki do TechNet: tópicos de solução de problemas [Solução de problemas do SSRS (SQL Server Reporting Services) no modo integrado do SharePoint](http://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [Fórum: SQL Server Reporting Services](http://social.msdn.microsoft.com/Forums/sqlreportingservices/threads)  
  
 ![Configurações do SharePoint](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configurações SharePoint") [enviar comentários e informações de contato pelo Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
  

