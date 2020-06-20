---
title: Gerenciador de Configurações do Reporting Services (modo nativo) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
ms.assetid: 379eab68-7f13-4997-8d64-38810240756e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f3dc4e2b2df66b9670bf00e39e6f4a2624c4105e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059057"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Gerenciador de Configurações do Reporting Services (Modo Nativo).
  Use o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no Modo Nativo. Se você instalou um servidor de relatório usando a opção de instalação somente arquivos, deverá usar o Gerenciador de Configuração para configurar o servidor antes de poder usá-lo. Se você instalou um servidor de relatório usando a opção de instalação de configuração padrão, poderá usar o Gerenciador de Configurações para verificar ou modificar as configurações que foram especificadas durante a instalação. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode ser usado para configurar uma instância local ou remota do servidor de relatório.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.  
  
> [!NOTE]  
>  A partir da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não foi desenvolvido para gerenciar servidores de relatório no modo do SharePoint. O modo do SharePoint é gerenciado e configurado por meio de scripts da Administração Central do SharePoint e do PowerShell. Para obter informações, consulte [Reporting Services instalação do modo sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
 **Nesta seção:**  
  
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 Fornece recomendações e etapas sobre como modificar a conta do serviço e a senha.  
  
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 Descreve como configurar as URLs usadas para acessar o serviço Web Servidor de Relatórios e o Gerenciador de Relatórios.  
  
 [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 Descreve como criar um banco de dados de servidor de relatório, exigido por armazenar metadados e objetos de servidor.  
  
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 Descreve como modificar a cadeia de conexão usada pelo servidor de relatório para conexão com o banco de dados do servidor de relatório.  
  
 [Configurar a conta de execução autônoma &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 Descreve como configurar uma conta do usuário para processar relatórios no modo autônomo.  
  
 [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 Descreve como configurar um servidor de relatório para dar suporte à distribuição de relatório por email.  
  
 [Configurar uma implantação de expansão do servidor de relatório no modo nativo &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 Fornece informações sobre como configurar várias instâncias do servidor de relatório para usar um banco de dados de servidor de relatório compartilhado.  
  
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
 Explica como usar e gerenciar as chaves de criptografia utilizadas ao armazenar dados confidenciais.  
  
 [Gerenciar um servidor de relatórios de Modo Nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
 Fornece instruções passo a passo para tarefas comuns.  
  
 [Gerenciador de Configurações do Reporting Services F1 tópicos de ajuda &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
 Fornece tópicos de ajuda para as páginas da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 **Neste tópico:**  
  
-   [Cenários a serem usados Gerenciador de Configurações do Reporting Services](#bkmk_scenarios)  
  
-   [Requisitos](#bkmk_requirements)  
  
-   [Para iniciar o Gerenciador de Configuração do Reporting Services](#bkmk_start_configuration_manager)  
  
##  <a name="scenarios-to-use-reporting-services-configuration-manager"></a><a name="bkmk_scenarios"></a> Cenários para usar o Gerenciador de Configuração do Reporting Services.  
 Você pode usar a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para executar as seguintes tarefas:  
  
-   Configurar a conta de serviço do Servidor de Relatório. A conta é configurada inicialmente durante a instalação, mas pode ser modificada usando a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se você atualizar a senha ou quiser usar uma conta diferente.  
  
-   Crie e configure os URLs. O servidor de relatório e o Gerenciador de Relatórios são aplicativos [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] acessados através de URLs. O URL do servidor de relatório fornece acesso aos pontos de extremidade SOAP do servidor de relatório. O URL do Gerenciador de Relatórios é usado para abri-lo. Você pode configurar um único URL ou vários URLs para cada aplicativo.  
  
-   Crie e configure o banco de dados de servidor de relatório. O servidor de relatório é um servidor sem monitoração de estado que requer um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenamento interno. Você pode usar a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar e configurar uma conexão ao banco de dados do servidor de relatório. Você também pode selecionar um banco de dados de servidor de relatório existente que já tenha o conteúdo você deseja usar.  
  
-   Configure uma implantação de expansão no modo Nativo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oferece suporte a uma topologia de implantação que permite que várias instâncias do servidor de relatório usem um único banco de dados de servidor de relatório compartilhado. Para fazer uma implantação de expansão de servidor de relatório, use a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para conectar cada servidor de relatório ao banco de dados de servidor de relatório compartilhado.  
  
-   Faça backup, restaure ou substitua a chave simétrica que é usada para criptografar cadeias de caracteres e credenciais de conexões armazenadas. Você deve ter uma cópia de backup da chave simétrica caso altere a conta de serviço ou mova um banco de dados do servidor de relatório para outro computador.  
  
-   Configure a conta de execução autônoma. Essa conta é usada para conexões remotas durante operações agendadas ou quando as credenciais de usuário não estão disponíveis.  
  
-   Configure o email do servidor de relatório. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email do servidor de relatório que usa o protocolo SMTP para entregar relatórios ou notificação de processamento de relatórios a uma caixa de correio eletrônica. Você pode usar o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar qual servidor ou gateway SMTP na sua rede será usado para entrega de e-mail.  
  
 A ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não o ajuda a gerenciar o conteúdo do servidor de relatório, habilitar recursos adicionais ou conceder acesso ao servidor. A implantação completa requer que você também use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para habilitar recursos adicionais ou modificar valores padrão e Report Manager para conceder acesso de usuário ao servidor.  
  
##  <a name="requirements"></a><a name="bkmk_requirements"></a> Requisitos  
 O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é específico da versão. O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalada com esta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser usado para configurar uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se você estiver executando versões mais antigas e mais novas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] lado a lado no mesmo computador, deverá usar o Gerenciador de Configurações do Reporting Services fornecido com cada versão para configurar cada instância.  
  
 Para usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você deve ter o seguinte:  
  
-   Permissões de administrador de sistema local no computador que hospeda o servidor de relatório que você deseja configurar. Se você estiver configurando um computador remoto, deverá ter permissões de administrador de sistema locais nesse computador também.  
  
-   É necessário ter permissão para criar bancos de dados no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usado para hospedar o banco de dados do servidor de relatório.  
  
-   O serviço WMI (Instrumentação de Gerenciamento do Windows) deve ser ativado e executado em qualquer servidor de relatório que você estiver configurando. O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa o provedor WMI do servidor de relatório para se conectar a servidores de relatório locais e remotos. Se você estiver configurando um servidor de relatório remoto, o computador deverá conceder acesso WMI remoto. Para obter mais informações, consulte [Configurar um Servidor de Relatório para Administração Remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
-   Antes de conectar-se a e configurar uma instância remota do servidor de relatório, você deve habilitar as chamadas remotas à WMI (Instrumentação de Gerenciamento do Windows) para passar pelo o Firewall do Windows. Para obter mais informações, consulte [Configurar um Servidor de Relatório para Administração Remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado automaticamente quando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
##  <a name="to-start-the-reporting-services-configuration-manager"></a><a name="bkmk_start_configuration_manager"></a>Para iniciar o Gerenciador de Configurações do Reporting Services  
  
#### <a name="to-start-reporting-services-configuration"></a>Para iniciar a Configuração do Reporting Services  
  
1.  Use a seguinte etapa que for apropriada para sua versão do Microsoft Windows:  
  
    -   Na tela inicial do Windows, digite **Relatórios** e selecione **Gerenciador de Configurações do Reporting Services** nos resultados da pesquisa.  
  
    -   Clique em **Iniciar**, aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]e aponte para **Ferramentas de Configuração**.  
  
         Para configurar uma instância do servidor de relatório de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra a pasta do programa dessa versão. Por exemplo, aponte para [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , em vez de [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] para abrir as ferramentas de configuração para os componentes de servidor do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
         Clique em **Gerenciador de Configuração do Reporting Services**.  
  
2.  A caixa de diálogo **Conexão de Configuração do Reporting Services** será exibida, para que você possa selecionar a instância do servidor de relatório que deseja configurar. Clique em **Conectar**.  
  
3.  Em **Nome do Servidor**, especifique o nome do computador no qual a instância do servidor de relatório está instalada. O nome do computador local aparece por padrão, mas você pode digitar o nome de uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar-se a um servidor de relatório que esteja instalado em um computador remoto.  
  
4.  Se você especificar um computador remoto, clique em **Localizar** para estabelecer uma conexão.  
  
5.  Em **Instância do Servidor de Relatório**, selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que deseja configurar. Somente instâncias de servidor de relatório para esta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparecem na lista. Você não pode configurar versões anteriores do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
6.  Clique em **Conectar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ferramentas de Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;Configuration Manager SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)   
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
