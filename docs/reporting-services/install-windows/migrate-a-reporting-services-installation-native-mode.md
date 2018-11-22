---
title: Migrar uma instalação do Reporting Services (Modo Nativo) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.date: 11/06/2018
ms.openlocfilehash: 67866bf7c201d9a00eb56195d3db10cdf272ef2b
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602936"
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>Migrar uma instalação do Reporting Services (Modo Nativo)

Este tópico contém instruções passo a passo sobre como migrar uma das seguintes versões com suporte de uma implantação de modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para uma nova instância do SQL Server Reporting Services:  
  
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
::: moniker-end

Para obter informações sobre como migrar uma implantação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , veja [Migrar uma instalação do Reporting Services &#40;modo do SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
 A migração é definida como a movimentação de arquivos de dados de aplicativo para uma nova instância do SQL Server. Estes são os motivos comuns para a migração da sua instalação:  
  
* Você tem uma implantação em grande escala ou requisitos de tempo de atividade.  
  
* Você está alterando o hardware ou a topologia da instalação.  
  
* Você detecta um problema que impede a atualização.

## <a name="bkmk_nativemode_migration_overview"></a> Visão geral da migração de modo nativo

 O processo de migração para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui etapas manuais e automatizadas. As seguintes tarefas fazem parte de uma migração de servidor de relatório:  
  
* Fazer backup de arquivos de banco de dados, de aplicativos e de configuração.  
  
* Fazer backup da chaves de criptografia.  
  
* Instalar uma nova instância do SQL Server. Se você estiver usando o mesmo hardware, poderá instalar o SQL Server lado a lado com a instalação existente se for uma das versões com suporte.  
  
    > [!TIP]  
    >  Uma instalação lado a lado pode exigir que você instale o SQL Server como uma instância nomeada.
  
* Mover o banco de dados do servidor de relatório e outros arquivos de aplicativo da instalação existente para a nova instalação do SQL Server.  
  
* Mover todos os arquivos de aplicativos personalizados para a nova instalação.  
  
* Configurar o servidor de relatório.  
  
* Edite **RSReportServer.config** para incluir todas as configurações personalizadas da instalação anterior.  
  
* Opcionalmente, configure listas de controle de acesso (ACLs) personalizadas para o novo grupo de serviços do Windows do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
* Remover aplicativos e ferramentas não utilizados depois de confirmar que a nova instância está totalmente operacional.  
  
 Há restrições nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedam o banco de dados do servidor de relatório. Revise o tópico a seguir se você estiver reutilizando um banco de dados do servidor de relatório criado em uma instalação anterior.  
  
* [Criar um banco de dados do servidor de relatório](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
## <a name="bkmk_fixed_database_name"></a> Nome fixo do banco de dados

 Você não pode renomear o banco de dados de servidor de relatório. A identidade do banco de dados é registrada em procedimentos armazenados do servidor de relatório quando o banco de dados é criado. A renomeação dos bancos de dados primário ou temporário do servidor de relatório ocasiona erros quando os procedimentos são executados, invalidando a instalação do servidor de relatório.  
  
 Se o nome do banco de dados da instalação existente não for adequado para a nova instalação, avalie a possibilidade de criar um novo banco de dados com o nome desejado e, em seguida, carregue os dados de aplicativo existentes usando as técnicas descritas na lista a seguir:  
  
* Grave um script do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que chame métodos SOAP do serviço Web Servidor de Relatórios para copiar dados entre bancos de dados. Use o utilitário RS.exe para executar o script. Para obter mais informações sobre essa abordagem, veja [Script e PowerShell com o Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md).  
  
* Grave o código que chama o provedor WMI para copiar dados entre bancos de dados. Para obter mais informações sobre essa abordagem, veja [Acessar o provedor WMI do Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
* Se houver poucos itens, você poderá republicar relatórios, modelos de relatório e fontes de dados compartilhadas do Designer de Relatórios, do Designer de Modelo e do Construtor de Relatórios no novo servidor de relatório. Recrie atribuições de função, assinaturas, agendamentos compartilhados, agendamentos de instantâneo, propriedades personalizadas definidas em relatórios ou outros itens, segurança de item de modelo e propriedades definidas no servidor de relatório. Esteja preparado para perder o histórico de relatórios e os dados de log de execução de relatório se você seguir essas ações.
  
## <a name="bkmk_before_you_start"></a> Antes de iniciar

 Embora você esteja migrando e não atualizando a instalação, considere a possibilidade de executar o Supervisor de Atualização na instalação existente para identificar problemas que poderiam afetar a migração. Esta etapa será especialmente útil se você estiver migrando um servidor de relatório que não instalou ou configurou. Ao executar o Supervisor de Atualização, você poderá obter informações sobre configurações personalizadas que podem não ter suporte em uma nova instalação do SQL Server.  
  
 Além disso, você deve estar ciente de várias alterações importantes feitas no SQL Server Reporting Services que afetam a maneira como a instalação é migrada:

* O novo [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] substituiu o Gerenciador de Relatórios.
  
* Desde o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o IIS não é mais um pré-requisito. Se você estiver migrando uma instalação do servidor de relatório para um novo computador, não precisará adicionar a função de servidor Web. Além disso, as etapas para configurar URLs e a autenticação são diferentes da versão anterior, assim como as técnicas e ferramentas usadas para diagnosticar e solucionar problemas.  
  
* O serviço Web Servidor de Relatório, o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]e o serviço Servidor de Relatório do Windows são executados na mesma conta. Todos os três aplicativos leem parâmetros de configuração do arquivo RSReportServer.config.
  
* O [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] e o SQL Server Management Studio foram reformulados para remover recursos sobrepostos. Cada ferramenta dá suporte a um conjunto distinto de tarefas.
  
* Os filtros ISAPI não têm suporte no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e em versões posteriores. Se você usa filtros ISAPI, deve remodelar sua solução de relatório antes de migração.  
  
* As restrições de endereço IP não têm suporte no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e em versões posteriores. Se você usa restrições de endereço IP, deve remodelar sua solução de relatório antes da migração ou usar uma tecnologia, como um firewall, um roteador ou a conversão de endereço de rede (NAT), para configurar endereços que tem restrições de acesso ao servidor de relatório.  
  
* Não há suporte para certificados SSL (protocolo SSL) de cliente no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e em versões posteriores. Se você usa certificados SSL de cliente, deve remodelar sua solução de relatório antes de migração.  
  
* Se você usar um tipo de autenticação diferente da autenticação integrada do Windows, deverá atualizar o elemento `<AuthenticationTypes>` no arquivo **RSReportServer.config** com um tipo de autenticação com suporte. Os tipos de autenticação que têm suporte são NTLM, Kerberos, Negotiate e Básica. Os tipos de autenticação Anônima, .NET Passport e Digest não têm suporte no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e em versões posteriores.  
  
* Se você usar folhas de estilos em cascata personalizadas em seu ambiente de relatório, elas não poderão ser migradas. Mova-as manualmente após a migração.
  
Para obter mais informações sobre as alterações no SQL Server Reporting Services, veja a documentação do Supervisor de Atualização e [Novidades no Reporting Services](../../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).  

## <a name="bkmk_backup"></a> Arquivos e dados para backup

 Antes de instalar uma nova instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], faça backup de todos os arquivos da instalação atual.  
  
1. Faça backup da chave de criptografia do banco de dados do servidor de relatório. Esta etapa é fundamental para o sucesso da migração. Mais adiante no processo de migração, você deverá restaurar a chave de criptografia para que o servidor de relatório tenha novamente acesso aos dados criptografados. Para fazer backup da chave, use o Gerenciador de Configurações do Reporting Services.  
  
2. Faça backup do banco de dados do servidor de relatório usando qualquer um dos métodos suportados de backup de bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, confira as instruções sobre como fazer backup do banco de dados do servidor de relatório em [Movendo os bancos de dados do servidor de relatório para outro computador &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
3. Faça backup dos arquivos de configuração do servidor de relatório. Os arquivos dos quais deve ser feito backup incluem:  
  
    1. RSReportServer.config  
  
    2. Rswebapplication.config  
  
    3. Rssvrpolicy.config  
  
    4. Rsmgrpolicy.config  
  
    5. Reportingservicesservice.exe.config  
  
    6. Web.config para o aplicativo [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] do Servidor de Relatório.  
  
    7. Machine.config de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] caso ele tenha sido modificado para operações do servidor de relatório.  

## <a name="bkmk_install_ssrs"></a> Instale o SQL Server Reporting Services

 Instale uma nova instância do servidor de relatório no modo somente arquivos para que você possa configurá-la para usar valores diferentes do padrão. Para a instalação pela linha de comando, use o argumento **FilesOnly**. No Assistente de Instalação, selecione a **opção Instalar, mas não configurar**.  
  
 Clique em um destes links para exibir instruções sobre como instalar uma nova instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
* [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
* [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  

## <a name="bkmk_move_database"></a> Mover o banco de dados do servidor de relatório

 O banco de dados do servidor de relatório contém relatórios publicados, modelos, fontes de dados compartilhadas, agendas, recursos, assinaturas e pastas. Ele também contém propriedades do sistema e de itens e permissões para acessar conteúdo do servidor de relatório.  
  
 Se a migração envolve o uso de uma outra instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , você deverá mover o banco de dados do servidor de relatório para a nova instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se você estiver usando a mesma instância [!INCLUDE[ssDE](../../includes/ssde-md.md)] , vá para a seção [Mover assemblies ou extensões personalizadas](#bkmk_move_custom).  
  
 Para mover o banco de dados do servidor de relatório, siga estas etapas:
  
1. Escolha a instância [!INCLUDE[ssDE](../../includes/ssde-md.md)] a ser usada. O SQL Server Reporting Services exige que você use uma das seguintes versões para hospedar o banco de dados do servidor de relatório:  
  
    ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end

    ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  

    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  

    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end
  
2. Inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3. Crie **RSExecRole** nos bancos de dados do sistema caso o [!INCLUDE[ssDE](../../includes/ssde-md.md)] nunca tenha hospedado um banco de dados do servidor de relatório. Para mais informações, veja [Criar o RSExecRole](../../reporting-services/security/create-the-rsexecrole.md).  
  
4. Siga as instruções em [Movendo os bancos de dados do servidor de relatório para outro computador &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
 Lembre-se de que o banco de dados do servidor de relatório e o banco de dados temporário são interdependentes e devem ser movidos juntos. Não copie os bancos de dados; a cópia não transfere todas as configurações de segurança para a nova instalação. Não mova trabalhos do SQL Server Agent para operações de servidor de relatório agendadas. O servidor de relatório recria esses trabalhos automaticamente.  

## <a name="bkmk_move_custom"></a> Mover assemblies ou extensões personalizadas

 Se a instalação inclui extensões, itens de relatório ou assemblies personalizados, reimplante os componentes personalizados. Se você não estiver usando componentes personalizados, vá para a seção [Configurar o servidor de relatório](#bkmk_configure_reportserver).  
  
 Para reimplantar os componentes personalizados, siga estas etapas:  
  
1. Verifique se os assemblies têm suporte ou se precisam de recompilação:

    * As extensões de segurança personalizadas devem ser gravadas novamente usando a interface [IAuthenticationExtension2](https://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.iauthenticationextension2.aspx).
  
    * As extensões de renderização personalizadas para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser reescritas usando o ROM (Modelo de Objeto de Renderização).  
  
    * Os renderizadores HTML 3.2 e HTML OWC não têm suporte no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e em versões posteriores.  
  
    * Outros assemblies personalizados não devem exigir recompilação.  
  
2. Mova os assemblies para o novo servidor de relatório e para as pastas /bin. No SQL Server, os binários do servidor de relatório são localizados no seguinte local para a instância padrão do servidor de relatório:  
  
     `\Program files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3. Modifique os arquivos de configuração para adicionar entradas para o componente personalizado. As entradas variam de acordo com o tipo de assembly que você está usando. Para obter instruções sobre onde inserir arquivos e adicionar entradas de configuração, confira abaixo:  
  
    1. [Implantando um assembly personalizado](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
  
    2. [Como implantar um item de relatório personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3. [Implantando uma extensão de processamento de dados](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4. [Implantando uma extensão de entrega](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5. [Implantando uma extensão de renderização](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6. [Implementando uma extensão de segurança](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  

## <a name="bkmk_configure_reportserver"></a> Configurar o servidor de relatório

 Configure as URLs do serviço Web Servidor de Relatórios e do portal da Web e configure a conexão com o banco de dados do servidor de relatório.  
  
 Se você estiver migrando uma implantação em expansão, coloque todos os nós do servidor de relatório offline e migre um servidor de cada vez. Depois que o primeiro servidor de relatório for migrado e se conectar ao banco de dados de servidor de relatório, a versão desse banco de dados será automaticamente atualizada para a versão do banco de dados do SQL Server.  
  
> [!IMPORTANT]
>  Se qualquer um dos servidores de relatório da implantação em expansão estiver online e não foi migrado, poderá ocorrer uma exceção *rsInvalidReportServerDatabase* porque ele está usando um esquema mais antigo quando conectado ao atualizado.  

Se o servidor de relatório migrado estiver configurado como o banco de dados compartilhado para uma implantação em expansão, exclua todas as chaves de criptografia antigas da tabela **Keys** no banco de dados do **ReportServer** antes de configurar o serviço de servidor de relatório. Se as chaves não forem removidas, o servidor de relatório migrado tentará inicializar em modo de implantação em expansão. Para obter mais informações, consulte [Adicionar e remover chaves de criptografia para implantação escalável &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md) e [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).  

As chaves em expansão não podem ser excluídas com o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As chaves antigas devem ser excluídas da tabela **Keys** no banco de dados do **ReportServer** usando o SQL Server Management Studio. Exclua todas as linhas da tabela Keys. Essa ação desmarca a tabela e a prepara para restaurar apenas a chave simétrica, conforme documentado nas seguintes etapas.  

Antes de excluir as chaves, é recomendável primeiro fazer backup da chave de Criptografia Simétrica. Você pode usar o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para fazer backup da chave. Abra o Configuration Manager, clique na guia Chaves de Criptografia e clique no botão **Backup**. Você também pode gerar um script de comandos WMI para fazer backup da chave de criptografia. Para obter mais informações sobre o WMI, consulte [Método BackupEncryptionKey &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md).  
  
1. Inicie o Gerenciador de Configurações do Reporting Services e se conecte à instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalada. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2. Configure URLs para o servidor de relatório e o portal da Web. Para obter mais informações, veja [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3. Configure o banco de dados do servidor de relatório selecionando o banco de dados do servidor de relatório existente da instalação anterior. Após a configuração bem-sucedida, os serviços do servidor de relatório serão reiniciados e, uma vez estabelecida a conexão com o banco de dados do servidor de relatório, o banco de dados será automaticamente atualizado para o SQL Server Reporting Services. Para obter mais informações sobre como executar o Assistente para Alterar Banco de Dados, usado para criar ou selecionar um banco de dados do servidor de relatório, consulte [Criar um banco de dados de servidor de relatório do modo nativo](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4. Restaure as chaves de criptografia. Esta etapa é necessária para permitir a criptografia reversível em credenciais e cadeias de conexão pré-existentes que já estão no banco de dados do servidor de relatório. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
5. Se você instalou o servidor de relatório em um novo computador e está usando o Firewall do Windows, verifique se a porta TCP em que o servidor de relatório escuta está aberta. Por padrão, essa porta é a 80. Para obter instruções, veja [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
6. Se você desejar administrar localmente seu servidor de relatório de modo nativo, configure o sistema operacional para permitir a administração local com o portal da Web. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  

## <a name="bkmk_copy_custom_config"></a> Copiar parâmetros de configuração personalizados para o arquivo RSReportServer.config

Se você modificou os arquivos RSReportServer.config ou RSWebApplication.config na instalação anterior, deverá fazer as mesmas modificações no novo arquivo RSReportServer.config. A lista a seguir resume alguns dos motivos pelos quais você pode ter modificado o arquivo de configuração anterior e apresenta links para informações adicionais sobre como definir as mesmas configurações no SQL Server 2016.  
  
|Personalização|Informações|  
|-------------------|-----------------|  
|Entrega de email do Servidor de Relatório com configurações personalizadas|[Configurações de email * Modo nativo do Reporting Services](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|Configurações de informações de dispositivo|[Personalizar parâmetros de extensão de renderização em RSReportServer.config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)|

## <a name="bkmk_windowsservice_group"></a> Grupo de Serviços do Windows e ACLs de segurança

 No [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], há um grupo de serviços, o grupo de Serviços Windows do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], usado para criar ACLs de segurança para todos os arquivos, pastas e chaves do registro instalados com o SQL Server Reporting Services. Este nome de grupo do Windows aparece no formato SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>.  

## <a name="bkmk_verify"></a> Verificar a implantação

1. Teste os diretórios virtuais do servidor de relatório e do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] abrindo um navegador e digitando a URL. Para obter mais informações, veja [Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
2. Teste os relatórios e verifique se eles contêm os dados esperados. Revise as informações de fonte de dados para detectar se as informações de conexão de fonte de dados ainda estão especificadas. O servidor de relatório usa o modelo de objeto de relatório ao processar e renderizar relatórios, mas não substitui os constructos [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] com elementos de linguagem de definição do novo relatório. Para obter mais informações sobre como os relatórios existentes são executados em uma nova versão do servidor de relatório, consulte [Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md).  

## <a name="bkmk_remove_unused"></a> Remover programas e arquivos que não são usados

Depois de migrar o servidor de relatório com êxito para uma nova instância, é recomendável executar as etapas descritas a seguir para remover programas e arquivos que não são mais necessários.  
  
1. Desinstale a versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] caso não precise mais dela. Esta etapa não exclui os seguintes itens, mas você poderá removê-los manualmente se não precisar mais deles:  
  
    * O antigo banco de dados do Servidor de Relatório  
  
    * A função RsExec  
  
    * As contas de serviço do Servidor de Relatório  
  
    * O pool de aplicativos relacionado ao serviço Web Servidor de Relatórios  
  
    * Diretórios virtuais do Gerenciador de Relatórios e do servidor de relatório  
  
    * Arquivos de log do servidor de relatório  
  
2. Remova o IIS se você não precisar mais dele no computador.

## <a name="next-steps"></a>Próximas etapas

* [Migrar uma instalação do Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  
* [Banco de dados do Servidor de Relatório](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
* [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
* [Compatibilidade com versões anteriores do Reporting Services](../../reporting-services/reporting-services-backward-compatibility.md)   
* [Gerenciador de Configurações do Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
