---
title: Solucionar problemas de instalação de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a9415e7258216c975dd066995bf347deca1d623
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253204"
---
# <a name="troubleshoot-a-reporting-services-installation"></a>Solucionar um problema da instalação do Reporting Services
  Se você não puder instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devido a erros ocorridos durante a Instalação, use as instruções deste tópico para identificar as condições mais prováveis que causam erros de instalação.  
  
 Para obter as informações mais recentes sobre problemas com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [Dicas, truques e soluções de problemas do Reporting Services SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=221297)  
  
 Para obter informações sobre outros erros e problemas relacionados ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte [Solução de problemas e erros do SSRS.](https://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx)  
  
 Examine as [notas de versão online](https://go.microsoft.com/fwlink/?linkid=236893) caso o problema encontrado seja descrito nas notas de versão.  
  
 Este tópico inclui as informações a seguir:  
  
-   [Verificar logs de instalação](#bkmk_setuplogs)  
  
-   [Verificar pré-requisitos](#bkmk_prereq)  
  
-   [Solucionar problemas com instalações do modo do SharePoint](#bkmk_tshoot_sharepoint)  
  
-   [Solucionar problemas com as instalações do modo nativo](#bkmk_tshoot_native)  
  
-   [Recursos adicionais](#bkmk_additional)  
  
##  <a name="bkmk_setuplogs"></a>Verificar logs de instalação  
 Os erros de instalação são registrados em arquivos de log na pasta **Arquivos de Programas\Microsoft SQL Server\110\Setup Bootstrap\Log** . Uma subpasta é criada toda vez que você executa a Instalação. O nome da subpasta é a hora e a data em que você executou a Instalação. Para obter instruções sobre como exibir os arquivos de log da Instalação, veja [Exibir e ler os arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
-   Os arquivos de log incluem uma coleção de arquivos.  
  
-   Abra o arquivo * _summary.txt para exibir informações sobre o produto, o componente e a instância.  
  
-   Abra o arquivo * _errorlog.txt para exibir informações de erro geradas durante a Instalação.  
  
-   Abra o arquivo *_RS\_\*_ComponentUpdateSetup.log para ver informações da instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
##  <a name="bkmk_prereq"></a>Verificar pré-requisitos  
 A Instalação verifica os pré-requisitos automaticamente. Entretanto, se você estiver solucionando problemas de instalação, será útil saber quais requisitos a Instalação está verificando.  
  
-   Os requisitos de conta para executar a Instalação inclui associação no grupo Administradores local. A Instalação deve ter permissão para adicionar arquivos, configurações de registro, criar grupos de segurança locais e definir permissões. Se você estiver instalando uma configuração padrão, a instalação deverá ter permissão para criar um banco de dados de servidor de relatório na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que será feita a instalação.  
  
-   O Sistema Operacional deve dar suporte a HTTP.SYS 1.1.  
  
-   O serviço HTTP deve estar habilitado e em execução.  
  
-   O DTC (Coordenador de Transações Distribuídas) deve estar em execução se você também estiver instalando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   Authz.dll deve estar presente na pasta System32.  
  
 A instalação não verifica mais Serviços de Informações da Internet (IIS) nem [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]requer o MDAC 2,0 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] a versão 2,0; A instalação irá instalá-las se ainda não estiverem instaladas.  
  
##  <a name="bkmk_tshoot_sharepoint"></a>Solucionar problemas com instalações do modo do SharePoint  
  
-   [Gerenciador de Configurações do Reporting Services não inicia](#bkmk_configmanager_notstart)  
  
-   [O serviço do SQL Server Reporting Services não é exibido na Administração Central do SharePoint após a instalação do SQL Server 2012 SSRS no modo do SharePoint](#bkmk_no_ssrs_service)  
  
-   [Reporting Services cmdlets do PowerShell não estão disponíveis e os comandos não são reconhecidos](#bkmk_cmdlets_not_recognized)  
  
-   [Você verá uma mensagem de erro indicando que a URL não está configurada](#bkmk_URL_not_configured)  
  
-   [A instalação falha em um computador com o SharePoint instalado, mas ele não está configurado](#bkmk_sharepoint_not_confiugred)  
  
-   [A página de administração central do SharePoint está em branco](#bkmk_central_admin_blank)  
  
-   [Você verá uma mensagem de erro ao tentar criar um novo relatório de Construtor de Relatórios](#bkmk_reportbuilder_newreport_error)  
  
-   [Você verá uma mensagem de erro informando que não há suporte para RS_SHP com PREPAREIMAGE](#bkmk_RS_SHP_notsupported)  
  
###  <a name="bkmk_configmanager_notstart"></a>Gerenciador de Configurações do Reporting Services não inicia  
 **Descrição:** Esse problema é por design no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] agora é arquitetado para a arquitetura de serviço do SharePoint. O Gerenciador de Configuração não é mais necessário para configurar e administrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo SharePoint.  
  
 **Solução alternativa:** Use a administração central do SharePoint para configurar um servidor de relatório no modo do SharePoint. Para obter mais informações, veja [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
###  <a name="bkmk_no_ssrs_service"></a>Você não vê o serviço de SQL Server Reporting Services na administração central do SharePoint após a instalação do SQL Server 2012 SSRS no modo do SharePoint  
 **Descrição:** Se, depois de instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com êxito o no modo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SharePoint e o suplemento para SharePoint 2010, você não vir "SQL Server Reporting Services" nos dois menus a seguir, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço não foi registrado:  
  
-   Administração Central do SharePoint 2010-> "gerenciamento de aplicativos" – > página "gerenciar serviços no servidor"  
  
-   Administração Central do SharePoint 2010-> "gerenciamento de aplicativos"-> "gerenciar aplicativos de serviço"-> menu "novo"  
  
 **Solução alternativa:** Para registrar e iniciar os [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviços do SharePoint, conclua o seguinte:  
  
1.  No computador que executa a Administração Central do SharePoint 2010  
  
    1.  Abra o Shell de Gerenciamento do SharePoint 2010 com privilégios de administrador. Clique com o botão direito no ícone e clique em "Executar como administrador". Execute os três cmdlets a seguir do shell:  
  
    2.  ```powershell
        Install-SPRSService  
        ```  
  
    3.  ```powershell
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```powershell
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  Verifique se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o serviço mostra o status como "**iniciado**" na página: administração central do SharePoint 2010-> "**gerenciamento de aplicativos**"-> "**gerenciar serviços no servidor**"  
  
###  <a name="bkmk_cmdlets_not_recognized"></a>Reporting Services cmdlets do PowerShell não estão disponíveis e os comandos não são reconhecidos  
 **Descrição:** Ao tentar executar um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cmdlet do PowerShell, você verá uma mensagem de erro semelhante à seguinte:  
  
-   O termo 'Install-SPRSServiceInstall-SPRSService' **não é reconhecido** como nome de um cmdlet, função, arquivo de script ou programa operável. Verifique a ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está correto e tente novamente.At line:1 char:39+ Install-SPRSServiceInstall-SPRSService <<<<    + CategoryInfo          : ObjectNotFound: (Install-SPRSServiceInstall-SPRSService:String) [], CommandNotFoundExcep  
  
 **Solução alternativa:** Conclua um dos seguintes:  
  
-   Execute o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint. **rsSharepoint. msi**.  
  
-   Instale o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da mídia de instalação do SQL Server.  
  
 **Observação:** Se o **Shell de gerenciamento do SharePoint 2013** estiver aberto quando você concluir uma das soluções alternativas, feche e reabra o Shell de gerenciamento.  
  
 Para saber mais, consulte o seguinte:   
  
-   [Onde encontrar o suplemento de Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Instalar o Reporting Services modo do SharePoint para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
-   [Instalar o Reporting Services SharePoint Mode para SharePoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
###  <a name="bkmk_URL_not_configured"></a>Você verá uma mensagem de erro indicando que a URL não está configurada  
 **Descrição:** Você vê e uma mensagem de erro semelhante à seguinte:  
  
 Essa funcionalidade do SSRS (SQL Server Reporting Services) não tem suporte. Use a Administração Central para verificar e corrigir um ou mais dos seguintes problemas:•Uma URL do servidor de relatório não está configurada. Use a página Integração do SSRS para defini-lo.•O proxy do aplicativo de serviço SSRS não está configurado. Use as páginas do aplicativo de serviço do SSRS para configurar o proxy.•O aplicativo de serviço SSRS não está mapeado para esse aplicativo web. Use as páginas do aplicativo de serviço do SSRS para associar o proxy do aplicativo de serviço SSRS ao Grupo Proxy de Aplicativo para esse aplicativo web.  
  
 **Solução alternativa:** A mensagem de erro contém três etapas sugeridas para corrigir esse problema. A primeira sugestão na mensagem "uma URL do servidor de relatório não está configurada..." é relevante ao integrar a versão do servidor de relatório anterior para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. A Configuração do SharePoint para as versões de servidor de relatório anteriores é concluída na página **Configurações Gerais do Aplicativo** , usando **SQL Server Reporting Services (2008 e 2008 R2)**.  
  
 **Mais informações:** Você verá essa mensagem de erro ao tentar usar qualquer uma das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] funcionalidades que exigem uma conexão com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço. Isso inclui:  
  
-   Abrindo o Construtor de Relatórios do SQL Server de uma biblioteca de documentos do SharePoint.  
  
-   Gerenciar assinaturas.  
  
-   Gerenciar um aplicativo de serviço.  
  
###  <a name="bkmk_sharepoint_not_confiugred"></a>A instalação falha em um computador com o SharePoint instalado, mas ele não está configurado  
 **Descrição:** Se você optar por instalar Reporting Services o modo do SharePoint em um computador que tenha o SharePoint instalado, mas o SharePoint não estiver configurado, você verá uma mensagem semelhante à seguinte e a instalação será interrompida:  
  
 A Instalação do SQL Server parou de funcionar  
  
 **Solução alternativa:** Configure o SharePoint e execute SQL Server instalação.  
  
 **Mais informações:** Ao instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o no e a instalação existente do SharePoint, a instalação tenta instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e iniciar o serviço do SharePoint. Se o SharePoint não estiver configurado, ocorrerá falha na instalação do serviço, e a instalação não será concluída.  
  
###  <a name="bkmk_central_admin_blank"></a>A página de administração central do SharePoint está em branco  
 **Descrição:** Você conseguiu instalar o SharePoint 2010 com êxito, sem erros de instalação. No entanto, quando você navega até a Administração Central, vê somente uma página em branco:  
  
 **Solução alternativa:** Esse problema não é específico do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , mas está relacionado à configuração de permissões em sua instalação geral do SharePoint. Esta é uma lista de sugestões:  
  
-   Examine o tópico do SharePoint sobre ambientes de desenvolvimento. [Configurando o ambiente de desenvolvimento para SharePoint 2010 no Windows Vista, no Windows 7 e no Windows Server 2008](https://msdn.microsoft.com/library/ee554869\(office.14\).aspx)  
  
-   Examine a publicação do fórum: [Administração Central retorna página em branco depois da instalação no Windows 7](https://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)  
  
-   A conta Serviço que você está usando para serviços do SharePoint como o Serviço de Administração Central do SharePoint 2010 deve ter privilégios administrativos no sistema operacional local.  
  
###  <a name="bkmk_reportbuilder_newreport_error"></a>Você verá uma mensagem de erro ao tentar criar um novo relatório de Construtor de Relatórios  
 **Descrição:** Você verá uma mensagem de erro semelhante à seguinte quando tentar criar um relatório de Construtor de Relatórios dentro de uma biblioteca de documentos:  
  
 Essa funcionalidade não tem suporte porque o aplicativo de serviço do SQL Server Reporting Services não existe ou uma URL do servidor de relatórios não foi configurada na Administração Central.  
  
 **Solução alternativa:** Verifique se você tem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] um aplicativo de serviço e se ele está configurado corretamente. Para obter mais informações, consulte a seção ' criar um aplicativo de serviço de Reporting Services ' em [instalar Reporting Services modo do SharePoint para sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
###  <a name="bkmk_RS_SHP_notsupported"></a>Você verá uma mensagem de erro informando que não há suporte para RS_SHP com PREPAREIMAGE  
 **Descrição:** Ao tentar executar o PREPAREIMAGE para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] você, você verá uma mensagem de erro semelhante à seguinte:  
  
 "O recurso 'RS_SHP' especificado não tem suporte ao executar a ação PREPAREIMAGE, porque ele não dá suporte a SysPrep. Remova os recursos que não são compatíveis com SysPrep e execute a instalação novamente."  
  
 **Solução alternativa:** Não há nenhuma solução alternativa. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte a SYSPREP (PREPAREIMAGE). 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Native oferece suporte a SYSPREP.  
  
##  <a name="bkmk_tshoot_native"></a>Solucionar problemas com as instalações do modo nativo  
  
###  <a name="PerfCounters"></a>Os contadores de desempenho não são visíveis após a atualização para o Windows Vista ou o Windows Server 2008  
 Se você atualizar o sistema operacional para [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] ou [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] em um computador que executa o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], os contadores de desempenho do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não serão definidos após a atualização.  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>Para instanciar novamente os contadores de desempenho do Reporting Services  
  
1.  Exclua as seguintes chaves do Registro:  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service**  
  
2.  Abra uma janela de comando e digite o seguinte comando no prompt:  
  
    -   **Execute \< ** o *diretório do .NET 2,0 Framework* **> \< ** *diretório bin do servidor de relatório* \installutil.exe **> \reportingserviceslibrary.dll**  
  
        > [!NOTE]  
        >  Substitua \<o *diretório .NET 2,0 Framework*> pelo caminho físico dos arquivos .NET Framework 2,0 e substitua \<o *diretório bin do servidor de relatório*> pelo caminho físico dos arquivos bin do servidor de relatório.  
  
3.  Reinicie o serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para verificar se as etapas funcionam, abra um navegador da Web e navegue até o URL do Gerenciador de Relatórios ou URL do Servidor de Relatório. Abra o Monitor de Desempenho para verificar se os contadores estão funcionando.  
  
#### <a name="to-re-add-the-performance-registry-keys-by-using-registry-editor"></a>Para adicionar novamente as chaves de Registro de desempenho usando o Editor do Registro  
  
1.  Abra o Editor do Registro:  
  
    1.  Clique em **Iniciar**e em **Executar**.  
  
    2.  Na caixa de diálogo **executar** , na caixa **abrir** , digite `regedit`.  
  
2.  No Editor do Registro, selecione a seguinte chave: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
3.  Clique com o botão direito do mouse no nó **Desempenho** , aponte para **Novo**e clique em **Valor com Várias Cadeias de Caracteres**.  
  
4.  Digite `Counter Names` e pressione Enter.  
  
5.  Repita para adicionar a chave de registro `Counter Types` nesse nó.  
  
6.  Navegue até esta chave de Registro: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
7.  Clique com o botão direito do mouse no nó **Desempenho** , aponte para **Novo**e clique em **Valor com Várias Cadeias de Caracteres**.  
  
8.  Digite `Counter Names` e pressione Enter.  
  
9. Repita para adicionar a chave de registro `Counter Types` nesse nó.  
  
 Depois que reparar a instância de 64 bits ou adicionar as chaves de Registro manualmente de novo, você poderá usar o Monitor de Desempenho para configurar os objetos de desempenho do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que deseja monitorar.  
  
###  <a name="ConfigPropsMissing"></a>As propriedades de configuração ReportServerExternalURL e PassThroughCookies não são configuradas após uma atualização do SQL Server 2005  
 Quando você atualiza do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], as propriedades de configuração `ReportServerExternalURL` e `PassThroughCookies` não são configuradas pelo processo de atualização. `ReportServerExternalURL`é uma propriedade opcional e deve ser definida somente se você estiver usando o SharePoint 2,0 Web Parts e desejar que os usuários possam recuperar um relatório e abri-lo em uma nova janela do navegador. Para obter mais informações `ReportServerExternalURL`sobre o, consulte [URLs em arquivos de configuração &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md). `PassThroughCookies`é necessário somente ao usar o método de autenticação personalizado. Para obter mais informações `PassThroughCookies`sobre o, consulte [Configurar Report Manager para passar cookies de autenticação personalizados](../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).  
  
> [!NOTE]  
>  Quando você usar a autenticação Personalizada, será recomendável migrar a instalação, em vez de executar uma atualização. Para obter mais informações sobre como migrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Migrar uma instalação do Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 Por padrão, essas propriedades não existem na configuração do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Caso você tenha configurado essas propriedades no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e continuar exigindo a funcionalidade fornecida por elas, adicione-as manualmente ao arquivo **RSReportServer.config** após o processo de atualização. Para obter mais informações, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
###  <a name="Default2005InstallBreaks2008"></a>A instalação falha para uma instância padrão do SQL Server 2005 Reporting Services em um computador que executa SQL Server serviços 2012Reportings  
 Se você tentar instalar uma instância [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] padrão do em um computador que já executa uma instância do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instância do não será instalada com a seguinte mensagem de erro:  
  
 "Já existe uma instância com o mesmo nome instalada neste computador. Para continuar com a Instalação do SQL Server, forneça um nome de instância exclusivo".  
  
 Esse problema ocorre se a instância do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] for uma instância nomeada padrão e mesmo que já exista uma instância do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] com esse nome no computador.  
  
 Para contornar esse problema, você dispõe das seguintes opções:  
  
-   Se for necessário executar [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o como a instância padrão no computador, você deverá instalar a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instância do antes [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] da instância do.  
  
-   Se a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instância não precisar ser uma instância padrão, você poderá instalar a instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como uma instância nomeada depois de instalar a instância [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] do.  
  
###  <a name="WindowsAuthBreaksAfterUpgrade"></a>401-erro não autorizado ao usar a autenticação do Windows após uma atualização do SQL Server 2005 para SQL Server 2012  
 Se você atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]o, e usar a autenticação NTLM com uma conta interna para a conta de serviço do servidor de relatório, poderá encontrar um erro 401-não autorizado ao acessar o servidor de relatório ou Report Manager após a atualização.  
  
 Isso ocorre devido a uma alteração na configuração padrão do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para autenticação do Windows. A negociação é configurada quando a conta do serviço Servidor de Relatórios é Serviço de Rede ou Sistema Local. O NTLM é configurado quando a conta do serviço Servidor de Relatórios não é uma dessas contas internas. Para corrigir o problema após atualizar, você pode editar o arquivo RSReportServer.config e configurar `AuthenticationType` para ser `RSWindowsNTLM`. Para obter mais informações, consulte [Configure Windows Authentication on the Report Server](../security/configure-windows-authentication-on-the-report-server.md).  
  
###  <a name="Uninstall32BitBreaks64Bit"></a>Desinstalando a instância de 32 bits do SQL Server 2012 Reporting Services na implantação lado a lado com uma instância do 64 bit interrompe a instância de 64 bits  
 Quando você instala uma instância de 32 bits e uma instância de 64 bits do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] lado a lado em um computador, e desinstalar a instância de 32 bits, quatro chaves do Registro do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são removidas. Isso trava a instância de 64 bits do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. As chaves do Registro do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que são removidas quando você desinstala a instância de 32 bits são:  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Types`  
  
 Para corrigir o problema, repare a instância de 64 bits. Embora seja recomendável usar o reparo, você pode adicionar outra vez as chaves do Registro manualmente usando o Editor do Registro.  
  
> [!CAUTION]  
>  A edição incorreta do Registro pode danificar seriamente o sistema. Antes de alterar o Registro, faça um backup dos dados importantes do computador.  
  
##  <a name="bkmk_additional"></a>Recursos adicionais  
 A seguir, veja os recursos adicionais que você pode examinar para auxiliá-lo com solução de problemas:  
  
-   Wiki do TechNet: tópicos de solução de problemas [Solução de problemas do SSRS (SQL Server Reporting Services) no modo integrado do SharePoint](https://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [Fórum: SQL Server Reporting Services](https://social.msdn.microsoft.com/Forums/sqlreportingservices/threads)  
  
