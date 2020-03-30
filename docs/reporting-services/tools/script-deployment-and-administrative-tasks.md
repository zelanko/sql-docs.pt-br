---
title: Implantação de script e tarefas administrativas | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- moving reports
- report servers [Reporting Services], duplicating settings
- deploying [Reporting Services], scripts
- copying report server settings
- administrative tasks [Reporting Services]
- duplicating report server environment
- migrating reports [Reporting Services]
- scripts [Reporting Services], deployments
- transferrng reports
- reports [Reporting Services], migrating
ms.assetid: d0416c9e-e3f9-456d-9870-2cfd2c49039b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 694a2c4c14564a1d3d57322e1300beddd8bfab98
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "66500575"
---
# <a name="script-deployment-and-administrative-tasks"></a>Implantação de script e tarefas administrativas

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte ao uso de scripts para automatizar a instalação, a implantação e as tarefas administrativas de rotina. A implantação de um servidor de relatórios é um processo de várias etapas. É preciso usar diversos processos e ferramentas para configurar uma implantação. Não existe nenhum programa ou abordagem que possa ser usado para automatizar todas as tarefas.  
  
 Não são todas as etapas que devem ser automatizadas. Em alguns casos, a abordagem mais simples e eficaz é executar uma etapa manualmente ou por meio de uma ferramenta gráfica. Por exemplo, se você deseja implantar uma grande quantidade de relatórios e modelos, é melhor copiar os bancos de dados do servidor de relatórios do que escrever um código que recrie o ambiente de servidor de relatórios.  
  
 Algumas etapas exigem um código personalizado. Por exemplo, a configuração das URLs para o serviço Web e o Gerenciador de Relatórios pode ser automatizada, mas apenas se você escrever o código personalizado que faz chamadas no provedor WMI (Instrumentação de Gerenciamento do Windows) do Servidor de Relatórios. Se você não quiser escrever código, utilize a ferramenta de Configuração [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para realizar a etapa.  
  
 Para executar o script que configure um servidor de relatórios, é necessário ser um administrador local no computador que você está configurando. Para obter mais informações, consulte [Configurar um Servidor de Relatório para Administração Remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
 Este tópico descreve abordagens recomendadas para automatizar etapas específicas. Diversos programas e interfaces programáticas são citados. Serão fornecidas descrições de cada um posteriormente neste tópico.  
  
## <a name="deployment-tasks-and-how-to-automate-them"></a>Tarefas de implantação e como automatizá-las  
 A tabela a seguir resume as tarefas de instalação e configuração necessárias para implantar um servidor de relatórios. Utilize a tabela para fazer a correspondência de uma tarefa específica a uma abordagem que permita automatizar ou realizar a tarefa autônoma.  
  
|Tarefa|Abordagem|  
|----------|--------------|  
|Instale o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|É possível executar a instalação da linha de comando para fazer uma instalação autônoma.<br /><br /> Utilize Instalação para instalar e configurar um servidor de relatório, mas apenas se você especificar a opção de configuração padrão e seu sistema atender todos os requisitos desse tipo de instalação. Caso não consiga instalar a configuração padrão, será preciso realizar uma instalação somente arquivos.|  
|Configure a conta de serviço.|A conta de serviço é configurada inicialmente por meio da Instalação. Para automatizar alterações na conta de serviço como uma tarefa pós-Instalação, é preciso escrever o código personalizado que faz chamadas no provedor WMI do Servidor de Relatórios. Não há nenhum utilitário de prompt de comando ou modelos de script para configurar a conta de serviço de forma programada.<br /><br /> Se os requisitos de codificação impedirem que você automatize esta etapa, você poderá facilmente configurar a conta manualmente executando a ferramenta de Configuração [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Configurar uma conta de serviço &#40; 	Gerenciador de Configurações do SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).|  
|Configure o serviço Web do Servidor de Relatórios e as URLs do Gerenciador de Relatórios.|Escreva o código personalizado que faz chamadas no provedor WMI do Servidor de Relatórios. Não há nenhum utilitário de linha de comando ou modelos de script para configurar as URLs.<br /><br /> Se preferir não escrever o código, você poderá configurar as URLs manualmente executando a ferramenta de Configuração [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, veja [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).|  
|Crie o banco de dados do servidor de relatórios.|Escreva o código personalizado que faz chamadas no provedor WMI do Servidor de Relatórios. Não há nenhum utilitário de prompt de comando ou modelos de script para criar os bancos de dados de servidor de relatórios e RSExecRole.<br /><br /> Se preferir não escrever o código, você poderá criar o banco de dados manualmente executando a ferramenta de Configuração [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Criar um banco de dados de servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).|  
|Configure a conexão do banco de dados do servidor de relatórios.|Se estiver alterando a cadeia de conexão, a conta, a senha ou o tipo de autenticação da conexão, execute o utilitário **rsconfig** para configurar a conexão. Para obter mais informações, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md) e [Utilitário rsconfig &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md).<br /><br /> Não é possível usar rsconfig.exe para criar ou atualizar o banco de dados. O banco de dados e a RSExecRole já devem existir.|  
|Configure uma implantação de expansão.|Escolha dentre as seguintes abordagens para automatizar a implantação de expansão:<br /><br /> -   Execute o utilitário rskeymgmt.exe para unir instâncias do servidor de relatório a uma instalação existente. Para obter mais informações, consulte [Adicionar e remover chaves de criptografia para implantação escalável &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).<br />-   Escreva o código personalizado executado no provedor WMI do Servidor de Relatório.|  
|Backup de chaves de criptografia.|Escolha dentre as seguintes abordagens para automatizar o backup da chave de criptografia:<br /><br /> -   Execute o utilitário rskeymgmt.exe para fazer o backup das chaves. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).<br />-   Escreva o código personalizado executado no provedor WMI do Servidor de Relatório.|  
|Configure o email do Servidor de Relatórios.|Escreva o código personalizado executado no provedor WMI [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O provedor oferece suporte a um subconjunto de configurações de email.<br /><br /> Embora o arquivo RSReportServer.config inclua todas as configurações, não utilize o arquivo de maneira automatizada. Mais especificamente, não use um arquivo em lotes para copiar o arquivo para outro servidor de relatórios. Cada arquivo de configuração inclui valores que são específicos à instância atual. Esses valores não serão válidos em outras instâncias de servidor de relatórios.<br /><br /> Confira mais informações em [Configurações de email – Modo nativo do Reporting Services (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|Configure a conta de execução autônoma.|Escolha dentre as seguintes abordagens para automatizar a configuração de conta de processamento autônoma:<br /><br /> -   Execute o utilitário rsconfig.exe para configurar a conta. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).<br />-   Escreva o código personalizado que faz chamadas no provedor WMI do Servidor de Relatório.|  
|Implemente o conteúdo existente em outro servidor de relatórios, incluindo a hierarquia de pastas, as atribuições de função, os relatórios, as assinaturas, as agendas, as fontes de dados e os recursos.|A melhor maneira de recriar um ambiente de servidor de relatórios existente é copiar o banco de dados do servidor de relatórios para uma nova instância de servidor de relatórios.<br /><br /> Outra opção é escrever o código personalizado que recria o conteúdo do servidor de relatórios existente de forma programada. No entanto, lembre-se que as assinaturas, os instantâneos de relatório e o histórico de relatórios não podem ser recriados de forma programada.<br /><br /> Algumas implantações se beneficiam de ambas as técnicas juntas (ou seja, restaurar um banco de dados do servidor de relatórios e, em seguida, executar o código personalizado que modifica o banco de dados do servidor de relatórios para uma instalação específica).<br /><br /> Para obter um exemplo detalhado, consulte [Script rs.exe do Reporting Services de exemplo para copiar conteúdo entre Servidores de Relatório](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).<br /><br /> Para obter mais informações sobre como relocar um banco de dados do servidor de relatório, consulte [Movendo os bancos de dados do servidor de relatório para outro computador &#40;Modo nativo do SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md). Para obter mais informações sobre a criação do ambiente do servidor de relatórios de forma programada, consulte a seção "Usando o script para migrar conteúdo e pastas do servidor de relatórios" neste tópico.|  
  
## <a name="tools-and-technologies-for-automating-server-deployment"></a>Ferramentas e tecnologias para automatizar a implantação do servidor  
 A lista a seguir resume os programas e as interfaces que podem ser usados para automatizar as tarefas de implantação e manutenção:  
  
-   O programa Instalação pode ser executado em modo autônomo para instalar e às vezes configurar os componentes do servidor de relatórios. Utilize a opção de instalação Somente Arquivos para que Instalação configure uma instância de servidor de relatórios.  
  
-   O provedor WMI [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e os utilitários de linha de comando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser usados para a configuração de servidor local e remota.  
  
     O provedor WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exibe classes, propriedades e métodos que permitem configurar todos os aspectos de uma instalação [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusive especificando a conta de serviço, as URLs de configuração, a criação e configuração do banco de dados do servidor de relatório ou a configuração de um servidor de relatório para envio de email. Escreva o código personalizado ou script para usar o provedor WMI. Para obter mais informações, consulte [Acessar o provedor WMI do Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
     Além de escrever o código, outra alternativa é usar os utilitários de linha de comando (rsconfig.exe e rskeymgmt.exe). Você pode gravar arquivos em lotes que executam os utilitários. É possível usar os utilitários para automatizar algumas, mas não todas as tarefas de configuração.  
  
-   A ferramenta de host de script (rs.exe) do servidor de relatório pode executar o código personalizado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que você talvez escreva para recriar ou transferir o conteúdo existente de um servidor de relatório para outro. Por essa abordagem, você escreve o script em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], o salva como arquivo .rss e usa o rs.exe para executar o script em um servidor de relatório de destino. O script escrito pode chamar a interface SOAP para o serviço Web do Servidor de Relatórios. Os scripts de implantação são escritos por meio dessa abordagem porque permitem recriar um espaço de trabalho e conteúdo de uma pasta de servidor de relatórios e recriar a segurança baseada na função.  
  
-   A versão SQL Server 2012 introduziu cmdlets do PowerShell para o modo integrado do SharePoint. Você pode usar o PowerShell para configurar e administrar a integração com o SharePoint.  Para obter mais informações, consulte [Cmdlets do PowerShell para o modo SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="use-scripts-to-migrate-report-server-content-and-folders"></a>Usar scripts para migrar conteúdo e pastas do servidor de relatório  
 Você pode escrever scripts que duplicam um ambiente de servidor de relatórios em outra instância de servidor de relatórios. Os scripts de implantação são, em geral, escritos em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e então processados usando o utilitário host do script do servidor de relatórios.  
  
 Para obter um exemplo detalhado, consulte [Script rs.exe do Reporting Services de exemplo para copiar conteúdo entre Servidores de Relatório](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Utilize scripts para copiar pastas, fontes de dados compartilhados, recursos, relatórios, atribuições de função e configurações de um servidor para outro. Você pode escrever um script para uma instância de servidor de relatórios e, em seguida, executá-lo em outro servidor para recriar o namespace do servidor de relatórios. Se possuir diversos servidores de relatórios em sua implantação [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você pode executar o script em cada servidor individualmente para configurar todos os servidores da mesma maneira.  
  
 A lista a seguir descreve as etapas da migração de relatórios de um servidor para outro.  
  
1.  Defina sua variável de script como a URL do servidor de relatório de fonte.  
  
2.  Use os métodos <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A> e <xref:ReportService2010.ReportingService2010.GetProperties%2A> para recuperar a definição e as propriedades do relatório.  
  
3.  Defina a URL para que aponte para o servidor de destino.  
  
4.  Use o método <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> , passando as propriedades retornadas por <xref:ReportService2010.ReportingService2010.GetProperties%2A> e a definição de relatório retornada por <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>.  
  
 Usando uma combinação dos métodos de obtenção e criação, é possível realizar etapas semelhantes para migrar configurações, pastas, fontes de dados compartilhados e recursos. Para obter mais informações sobre os métodos disponíveis, consulte [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md).  
  
> [!NOTE]  
>  Os scripts executados sob as credenciais do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows do usuário que está executando o script a menos que as credenciais estejam explicitamente configuradas.  
  
 Para obter mais informações sobre como formatar e executar um arquivo de script, consulte [Gerar scripts com o utilitário rs.exe e o serviço Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
## <a name="using-scripts-to-set-server-properties"></a>Usando scripts para configurar propriedades do servidor  
 Você pode escrever scripts que configuram as propriedades do sistema no servidor de relatórios. O script .NET [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] a seguir exibe um modo de configurar as propriedades. Este exemplo desabilita o controle ActiveX de RSClientPrint, mas é possível substituir **EnableClientPrinting** e **False** por qualquer nome e valor válido da propriedade. Para exibir uma lista completa das propriedades do servidor, consulte [Propriedades do sistema do servidor de relatório](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md).  
  
 Para usar o script, salve-o em um arquivo com extensão .rss e, em seguida, use o utilitário de prompt de comando rs.exe para executar o arquivo no servidor de relatórios. O script não é compilado, logo não é necessário ter uma instalação de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Este exemplo supõe que você possui permissões no computador local que hospeda o servidor de relatórios. Caso não esteja conectado por uma conta que possua permissões, é preciso especificar as informações de conta por meio de argumentos de linha de comando adicionais. Para obter mais informações, consulte [Utilitário RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md).  
  
> [!TIP]  
>  Para obter um exemplo detalhado, consulte [Script rs.exe do Reporting Services de exemplo para copiar conteúdo entre Servidores de Relatório](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
```  
Public Sub Main()  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
End Sub  
```

## <a name="next-steps"></a>Próximas etapas

[Método GenerateDatabaseCreationScript &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)   
[Método GenerateDatabaseRightsScript &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)   
[Método GenerateDatabaseUpgradeScript &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)   
[Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
[Instalar o servidor de relatórios de modo nativo do Reporting Services](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
[Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
[Utilitários de prompt de comando do servidor de relatório &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
[Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)   
[Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
