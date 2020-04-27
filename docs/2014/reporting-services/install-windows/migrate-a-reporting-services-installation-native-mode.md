---
title: Migrar uma instalação do Reporting Services (Modo Nativo) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.custom: ''
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.date: 08/10/2017
ms.openlocfilehash: c359f709b2c0a1ba779111a007843dd249b5d7b7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63261297"
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>Migrar uma instalação do Reporting Services (Modo Nativo)

  Este tópico fornece instruções passo a passo para migrar uma das seguintes versões com suporte de uma [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] implantação de modo nativo para uma nova [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instância do:  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)](Requer mais etapas, consulte [você não pode usar SQL Server 2005 para hospedar bancos de dados do servidor de relatório 2014](https://support.microsoft.com/kb/2796721).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.|  
  
 Para obter informações sobre como migrar uma implantação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , veja [Migrar uma instalação do Reporting Services &#40;modo do SharePoint&#41;](migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
 A migração é definida como a movimentação de arquivos de dados de aplicativo para uma nova instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Estes são os motivos comuns para a migração da sua instalação:  
  
-   Você tem uma implantação em grande escala ou requisitos de tempo de atividade.  
  
-   Você está alterando o hardware ou a topologia da instalação.  
  
-   Você detecta um problema que impede a atualização.  
  
##  <a name="native-mode-migration-overview"></a><a name="bkmk_nativemode_migration_overview"></a> Visão geral da migração de modo nativo  
 O processo de migração para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui etapas manuais e automatizadas. As seguintes tarefas fazem parte de uma migração de servidor de relatório:  
  
-   Fazer backup de arquivos de banco de dados, de aplicativos e de configuração.  
  
-   Fazer backup da chaves de criptografia.  
  
-   Instalar uma nova instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se você estiver usando o mesmo hardware, poderá instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] lado a lado com a instalação existente se for uma das versões com suporte.  
  
    > [!TIP]  
    >  Uma instalação lado a lado pode exigir que você instale o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] como uma instância nomeada.  
  
-   Mover o banco de dados do servidor de relatório e outros arquivos de aplicativo da instalação existente para a nova instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
-   Mover todos os arquivos de aplicativos personalizados para a nova instalação.  
  
-   Configurar o servidor de relatório.  
  
-   Edite **RSReportServer.config** para incluir todas as configurações personalizadas da instalação anterior.  
  
-   Opcionalmente, configure listas de controle de acesso (ACLs) personalizadas para o novo grupo de serviços do Windows do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Remover aplicativos e ferramentas não utilizados depois de confirmar que a nova instância está totalmente operacional.  
  
 Há restrições nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedam o banco de dados do servidor de relatório. Revise o tópico a seguir se você estiver reutilizando um banco de dados do servidor de relatório criado em uma instalação anterior.  
  
-   [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
  
##  <a name="fixed-database-name"></a><a name="bkmk_fixed_database_name"></a> Nome fixo do banco de dados  
 Você não pode renomear o banco de dados de servidor de relatório. A identidade do banco de dados é registrada em procedimentos armazenados do servidor de relatório quando o banco de dados é criado. A renomeação dos bancos de dados primário ou temporário do servidor de relatório ocasiona erros quando os procedimentos são executados, invalidando a instalação do servidor de relatório.  
  
 Se o nome do banco de dados da instalação existente não for adequado para a nova instalação, avalie a possibilidade de criar um novo banco de dados com o nome desejado e, em seguida, carregue os dados de aplicativo existentes usando as técnicas descritas na lista a seguir:  
  
-   Grave um script do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que chame métodos SOAP do serviço Web Servidor de Relatórios para copiar dados entre bancos de dados. Use o utilitário RS.exe para executar o script. Para obter mais informações sobre essa abordagem, veja [Script e PowerShell com o Reporting Services](../tools/scripting-and-powershell-with-reporting-services.md).  
  
-   Grave o código que chama o provedor WMI para copiar dados entre bancos de dados. Para obter mais informações sobre essa abordagem, veja [Acessar o provedor WMI do Reporting Services](../tools/access-the-reporting-services-wmi-provider.md).  
  
-   Se houver poucos itens, você poderá republicar relatórios, modelos de relatório e fontes de dados compartilhadas do Designer de Relatórios, do Designer de Modelo e do Construtor de Relatórios no novo servidor de relatório. Você deve recriar atribuições de função, assinaturas, agendas compartilhadas, agendas de instantâneo de relatório, propriedades personalizadas definidas em relatórios ou outros itens, segurança de item de modelo e propriedades definidas no servidor de relatório. Você perderá os dados do histórico de relatório e do log de execução de relatório.  
  
##  <a name="before-you-start"></a><a name="bkmk_before_you_start"></a> Antes de iniciar  
 Embora você esteja migrando e não atualizando a instalação, considere a possibilidade de executar o Supervisor de Atualização na instalação existente para identificar problemas que poderiam afetar a migração. Esta etapa será especialmente útil se você estiver migrando um servidor de relatório que não instalou ou configurou. Executando o Supervisor de Atualização, você poderá obter informações sobre configurações personalizadas que podem não ter suporte em uma nova instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Além disso, você deve estar ciente de várias alterações importantes feitas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que afetarão a maneira como a instalação será migrada:  
  
-   Desde o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o IIS não é mais um pré-requisito. Se você estiver migrando uma instalação do servidor de relatório para um novo computador, não precisará adicionar a função de servidor Web. Além disso, as etapas para configurar URLs e a autenticação são diferentes da versão anterior, assim como as técnicas e ferramentas usadas para diagnosticar e solucionar problemas.  
  
-   O serviço Web Servidor de Relatórios, o Gerenciador de Relatórios e o serviço do Servidor de Relatório do Windows foram consolidados em um único serviço Servidor de Relatório. Todos os três aplicativos são executados sob a mesma conta. Todos os três aplicativos leem parâmetros de configuração do arquivo RSReportServer.config, o que torna RSWebApplication.config obsoleto.  
  
-   O Gerenciador de Relatórios e o SQL Server Management Studio foram reformulados para remover recursos sobrepostos. Cada ferramenta é compatível com um conjunto distinto de tarefas; as ferramentas não são mais intercambiáveis.  
  
-   Os filtros ISAPI não são compatíveis com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versões posteriores. Se você usa filtros ISAPI, deve remodelar sua solução de relatório antes de migração.  
  
-   As restrições de endereço IP não são compatíveis com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versões posteriores. Se você usa restrições de endereço IP, deve remodelar sua solução de relatório antes da migração ou usar uma tecnologia, como um firewall, um roteador ou a conversão de endereço de rede (NAT), para configurar endereços que tem restrições de acesso ao servidor de relatório.  
  
-   Não há suporte para certificados de protocolo SSL de cliente ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SSL) no e em versões posteriores. Se você usa certificados SSL de cliente, deve remodelar sua solução de relatório antes de migração.  
  
-   Se você usar um tipo de autenticação diferente da autenticação integrada do Windows, atualize o elemento `<AuthenticationTypes>` no arquivo **RSReportServer.config** com um tipo de autenticação com suporte. Os tipos de autenticação que têm suporte são NTLM, Kerberos, Negotiate e Básica. Os tipos de autenticação Anônima, .NET Passport e Digest não são compatíveis com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versões posteriores.  
  
-   Se você usar folhas de estilos em cascata personalizadas no ambiente de relatório, elas não serão migradas. Você deverá movê-las manualmente após a migração.  
  
 Para obter mais informações sobre as [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]alterações no, consulte a documentação do supervisor de atualização e as novidades [&#40;Reporting Services&#41;](../what-s-new-reporting-services.md).  
  
##  <a name="backup-files-and-data"></a><a name="bkmk_backup"></a> Arquivos e dados para backup  
 Antes de instalar uma nova instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], faça backup de todos os arquivos da instalação atual.  
  
1.  Faça backup da chave de criptografia do banco de dados do servidor de relatório. Esta etapa é fundamental para o sucesso da migração. Mais adiante no processo de migração, você deverá restaurar a chave de criptografia para que o servidor de relatório tenha novamente acesso aos dados criptografados. Para fazer backup da chave, use o Gerenciador de Configurações do Reporting Services.  
  
2.  Faça backup do banco de dados do servidor de relatório usando qualquer um dos métodos suportados de backup de bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, confira as instruções sobre como fazer backup do banco de dados do servidor de relatório em [Movendo os bancos de dados do servidor de relatório para outro computador &#40;Modo Nativo do SSRS&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
3.  Faça backup dos arquivos de configuração do servidor de relatório. Os arquivos dos quais deve ser feito backup incluem:  
  
    1.  RSReportServer.config  
  
    2.  Rswebapplication.config  
  
    3.  Rssvrpolicy.config  
  
    4.  Rsmgrpolicy.config  
  
    5.  Reportingservicesservice.exe.config  
  
    6.  Web.config dos aplicativos Servidor de Relatório e Gerenciador de Relatórios do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] .  
  
    7.  Machine.config de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] caso ele tenha sido modificado para operações do servidor de relatório.  
  
##  <a name="install-sql-server-reporting-services"></a><a name="bkmk_install_ssrs"></a> Instale o SQL Server Reporting Services  
 Instale uma nova instância do servidor de relatório no modo somente arquivos para que você possa configurá-la para usar valores diferentes do padrão. Para fazer a instalação pela linha de comando, use o argumento `FilesOnly`. No Assistente de Instalação, selecione a **opção Instalar, mas não configurar**.  
  
 Clique em um destes links para exibir instruções sobre como instalar uma nova instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   [Instale o SQL Server 2014 do assistente de instalação &#40;a instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
-   [Install SQL Server 2014 from the Command Prompt](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
##  <a name="move-the-report-server-database"></a><a name="bkmk_move_database"></a> Mover o banco de dados do servidor de relatório  
 O banco de dados do servidor de relatório contém relatórios publicados, modelos, fontes de dados compartilhadas, agendas, recursos, assinaturas e pastas. Ele também contém propriedades do sistema e de itens e permissões para acessar conteúdo do servidor de relatório.  
  
 Se a migração envolve o uso de uma outra instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , você deverá mover o banco de dados do servidor de relatório para a nova instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se você estiver usando a mesma instância [!INCLUDE[ssDE](../../includes/ssde-md.md)] , vá para a seção [Mover assemblies ou extensões personalizadas](#bkmk_move_custom).  
  
 Para mover o banco de dados do servidor de relatório, faça o seguinte:  
  
1.  Escolha a instância [!INCLUDE[ssDE](../../includes/ssde-md.md)] a ser usada. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requer que você use uma das seguintes versões para hospedar o banco de dados do servidor de relatório:  
  
    -   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    -   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
2.  Inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3.  Crie `RSExecRole` nos bancos de dados do sistema caso o [!INCLUDE[ssDE](../../includes/ssde-md.md)] nunca tenha hospedado um banco de dados do servidor de relatório. Para mais informações, veja [Criar o RSExecRole](../security/create-the-rsexecrole.md).  
  
4.  Siga as instruções em [Movendo os bancos de dados do servidor de relatório para outro computador &#40;Modo Nativo do SSRS&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
 Lembre-se de que o banco de dados do servidor de relatório e o banco de dados temporário são interdependentes e devem ser movidos juntos. Não copie os bancos de dados; a cópia não transfere todas as configurações de segurança para a nova instalação. Não mova trabalhos do SQL Server Agent para operações de servidor de relatório agendadas. O servidor de relatório recriará esses trabalhos automaticamente.  
  
##  <a name="move-custom-assemblies-or-extensions"></a><a name="bkmk_move_custom"></a> Mover assemblies ou extensões personalizadas  
 Se a instalação inclui extensões, itens de relatório ou assemblies personalizados, reimplante os componentes personalizados. Se você não estiver usando componentes personalizados, vá para a seção [Configurar o servidor de relatório](#bkmk_configure_reportserver).  
  
 Para reimplantar os componentes personalizados, faça o seguinte:  
  
1.  Verifique se os assemblies têm suporte ou se precisam de recompilação:  
  
    -   As extensões de autenticação personalizadas que foram criadas para a versão [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] devem ser recompiladas.  
  
    -   As extensões de renderização personalizadas para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser reescritas usando o ROM (Modelo de Objeto de Renderização).  
  
    -   Os renderizadores HTML 3.2 e HTML OWC não são compatíveis com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versões posteriores.  
  
    -   Outros assemblies personalizados não devem exigir recompilação.  
  
2.  Mova os assemblies para o novo servidor de relatório e para as pastas /bin do Gerenciador de Relatórios. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os binários do servidor de relatório estão localizados no seguinte local para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a instância padrão:  
  
     `\Program files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3.  Modifique os arquivos de configuração para adicionar entradas para o componente personalizado. As entradas variarão de acordo com o tipo de assembly que você está usando. Para obter instruções sobre onde colocar arquivos e adicionar entradas de configuração, consulte o seguinte:  
  
    1.  [Implantando um assembly personalizado](../custom-assemblies/deploying-a-custom-assembly.md)  
  
    2.  [Como: implantar um Item de relatório personalizado](../custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3.  [Implantando uma extensão de processamento de dados](../extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4.  [Implantando uma extensão de entrega](../extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5.  [Implantando uma extensão de renderização](../extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6.  [Implementando uma extensão de segurança](../extensions/security-extension/implementing-a-security-extension.md)  
  
##  <a name="configure-the-report-server"></a><a name="bkmk_configure_reportserver"></a> Configurar o servidor de relatório  
 Configure as URLs do serviço Web Servidor de Relatórios e do Gerenciador de Relatórios e configure a conexão com o banco de dados do servidor de relatório.  
  
 Se você estiver migrando uma implantação em expansão, coloque todos os nós do servidor de relatório offline e migre um servidor de cada vez. Depois que o primeiro servidor de relatório for migrado e se conectar ao banco de dados de servidor de relatório, a versão desse banco de dados será automaticamente atualizada para a versão do banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
> [!IMPORTANT]  
>  Se qualquer um dos servidores de relatório da implantação em expansão estiver online e não foi migrado, poderá ocorrer uma exceção rsInvalidReportServerDatabase porque ele está usando um esquema mais antigo quando conectado ao atualizado.  
  
> [!NOTE]  
>  Se o servidor de relatório migrado foi configurado como o banco de dados compartilhado para uma implantação em expansão, exclua todas as chaves de criptografia antigas da tabela **Keys** no banco de dados do **ReportServer** , antes de configurar o serviço de servidor de relatório. Se as chaves não forem removidas, o servidor de relatório migrado tentará inicializar em modo de implantação em expansão. Para obter mais informações, consulte [Adicionar e remover chaves de criptografia para implantação escalável &#40;SSRS Configuration Manager&#41;](add-and-remove-encryption-keys-for-scale-out-deployment.md) e [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-manage-encryption-keys.md).  
>   
>  As chaves em expansão não podem ser excluídas com o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As chaves antigas devem ser excluídas da tabela **Keys** no banco de dados do **ReportServer** usando o SQL Server Management Studio. Exclua todas as linhas da tabela Keys. Isso desmarcará a tabela e a preparará para restaurar apenas a chave simétrica, conforme documentado nas etapas a seguir.  
>   
>  Antes de excluir as chaves, é recomendável primeiro fazer backup da chave de Criptografia Simétrica. Você pode usar o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para fazer backup da chave. Abra o Configuration Manager abrir, clique na guia **chaves de criptografia** e, em seguida, clique no botão **backup** . Você também pode gerar um script de comandos WMI para fazer backup da chave de criptografia. Para obter mais informações sobre o WMI, consulte [Método BackupEncryptionKey &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md).  
  
1.  Inicie o Gerenciador de Configurações do Reporting Services e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recém-instalada. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
2.  Configure URLs para o servidor de relatório e o Gerenciador de Relatórios. Para obter mais informações, veja [Configurar uma URL &#40;SSRS Configuration Manager&#41;](configure-a-url-ssrs-configuration-manager.md).  
  
3.  Configure o banco de dados do servidor de relatório selecionando o banco de dados do servidor de relatório existente da instalação anterior. Após a configuração bem-sucedida, os serviços do servidor de relatório serão reiniciados e, depois que uma conexão for feita com o banco de dados do servidor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]de relatório, o banco de dados será atualizado automaticamente para o. Para obter mais informações sobre como executar o Assistente para Alterar Banco de Dados, usado para criar ou selecionar um banco de dados do servidor de relatório, veja [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Restaure as chaves de criptografia. Esta etapa é necessária para permitir a criptografia reversível em credenciais e cadeias de conexão pré-existentes que já estão no banco de dados do servidor de relatório. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
5.  Se você instalou o servidor de relatório em um novo computador e está usando o Firewall do Windows, verifique se a porta TCP em que o servidor de relatório escuta está aberta. Por padrão, essa porta é a 80. Para obter instruções, veja [Configurar um firewall para acesso ao servidor de relatório](../report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Se você desejar administrar localmente seu servidor de relatório de modo nativo, configure o sistema operacional para permitir a administração local com o Gerenciador de Relatórios. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="copy-custom-configuration-settings-to-rsreportserverconfig-file"></a><a name="bkmk_copy_custom_config"></a> Copiar parâmetros de configuração personalizados para o arquivo RSReportServer.config  
 Se você modificou os arquivos RSReportServer.config ou RSWebApplication.config na instalação anterior, deverá fazer as mesmas modificações no novo arquivo RSReportServer.config. A lista a seguir resume alguns dos motivos pelos quais você pode ter modificado o arquivo de configuração anterior e apresenta links para informações adicionais sobre como definir as mesmas configurações no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Personalização|Informações|  
|-------------------|-----------------|  
|Entrega de email do Servidor de Relatório com configurações personalizadas|[Configurar um servidor de relatório para entrega de email &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [configurações de email-Configuration Manager &#40;modo nativo do SSRS&#41;](e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|Configurações de informações de dispositivo|[Personalizar parâmetros de extensão de renderização em RSReportServer.config](../customize-rendering-extension-parameters-in-rsreportserver-config.md)|  
|Gerenciador de Relatórios em uma instância remota|[Configurar o Gerenciador de Relatórios &#40;modo nativo&#41;](../report-server/configure-web-portal.md)|  
  
##  <a name="windows-service-group-and-security-acls"></a><a name="bkmk_windowsservice_group"></a> Grupo de Serviços do Windows e ACLs de segurança  
 No [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], há um grupo de serviços, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] grupo de serviços do Windows, que é usado para criar ACLs de segurança para todas as chaves, arquivos e pastas do registro instalados [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]com o. Este nome de grupo do Windows aparece no formato SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>. Esse grupo substitui os dois grupos de serviços do Windows no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se você tiver ACLs personalizadas associadas a qualquer um dos [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] grupos do Windows, será necessário aplicar essas ACLs ao novo grupo para a nova instância do servidor de relatório no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##  <a name="verify-your-deployment"></a><a name="bkmk_verify"></a> Verificar a implantação  
  
1.  Teste os diretórios virtuais do servidor de relatório e do Gerenciador de Relatórios abrindo um navegador e digitando a URL. Para obter mais informações, veja [Verificar uma instalação do Reporting Services](verify-a-reporting-services-installation.md).  
  
2.  Teste os relatórios e verifique se eles contêm os dados esperados. Revise as informações de fonte de dados para detectar se as informações de conexão de fonte de dados ainda estão especificadas. O servidor de relatório usa o modelo de objeto de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] quando processa e renderiza relatórios, mas não substitui construções do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por novos elementos RDL. Para obter mais informações sobre como os relatórios existentes são executados em um servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , veja [Atualizar relatórios](upgrade-reports.md).  
  
##  <a name="remove-unused-programs-and-files"></a><a name="bkmk_remove_unused"></a> Remover programas e arquivos que não são usados  
 Depois de migrar com êxito o servidor de relatório para uma [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instância do, talvez você queira executar as etapas a seguir para remover programas e arquivos que não são mais necessários.  
  
1.  Desinstale a versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] caso não precise mais dela. Esta etapa não exclui os seguintes itens, mas você poderá removê-los manualmente se não precisar mais deles:  
  
    -   O antigo banco de dados do Servidor de Relatório  
  
    -   A função RsExec  
  
    -   As contas de serviço do Servidor de Relatório  
  
    -   O pool de aplicativos relacionado ao serviço Web Servidor de Relatórios  
  
    -   Diretórios virtuais do Gerenciador de Relatórios e do servidor de relatório  
  
    -   Arquivos de log do servidor de relatório  
  
2.  Remova o IIS se você não precisar mais dele no computador.  
  
## <a name="see-also"></a>Consulte Também  
 [Migre uma instalação do Reporting Services &#40;modo do SharePoint&#41;](migrate-a-reporting-services-installation-sharepoint-mode.md)   
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [Atualizar e migrar Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [Compatibilidade com versões anteriores do Reporting Services](../reporting-services-backward-compatibility.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
