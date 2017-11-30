---
title: "Gerenciador de Configurações do Reporting Services (modo nativo) | Microsoft Docs"
ms.custom: 
ms.date: 09/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: e693575acb5c2eef31231a434dc25ee90b3ade36
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Gerenciador de Configurações do Reporting Services (Modo Nativo).

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Use o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no Modo Nativo. Se você instalou um servidor de relatório usando a opção de instalação somente arquivos, deverá usar o Gerenciador de Configuração para configurar o servidor antes de poder usá-lo. Se você instalou um servidor de relatório usando a opção de instalação de configuração padrão, poderá usar o Gerenciador de Configurações para verificar ou modificar as configurações que foram especificadas durante a instalação. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode ser usado para configurar uma instância local ou remota do servidor de relatório.

> [!NOTE]
> A partir da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não foi desenvolvido para gerenciar servidores de relatório no modo do SharePoint. O modo do SharePoint é gerenciado e configurado por meio de scripts da Administração Central do SharePoint e do PowerShell.  
  
##  <a name="bkmk_scenarios"></a> Cenários para usar o Gerenciador de Configuração do Reporting Services.  
 Você pode usar a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para executar as seguintes tarefas:  
  
-   Configurar a conta de serviço do Servidor de Relatório. A conta é configurada inicialmente durante a instalação, mas pode ser modificada usando a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se você atualizar a senha ou quiser usar uma conta diferente.  
  
-   Crie e configure os URLs. O servidor de relatório e o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] são aplicativos do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] acessados através de URLs. O URL do servidor de relatório fornece acesso aos pontos de extremidade SOAP do servidor de relatório. A URL [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] é usada para abrir o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] . Você pode configurar uma única URL ou várias URLs para cada aplicativo.  
  
-   Crie e configure o banco de dados de servidor de relatório. O servidor de relatório é um servidor sem monitoração de estado que requer um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenamento interno. Você pode usar a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar e configurar uma conexão ao banco de dados do servidor de relatório. Você também pode selecionar um banco de dados de servidor de relatório existente que já tenha o conteúdo você deseja usar.  
  
-   Configure uma implantação de expansão no modo Nativo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oferece suporte a uma topologia de implantação que permite que várias instâncias do servidor de relatório usem um único banco de dados de servidor de relatório compartilhado. Para fazer uma implantação de expansão de servidor de relatório, use a ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para conectar cada servidor de relatório ao banco de dados de servidor de relatório compartilhado.  
  
-   Faça backup, restaure ou substitua a chave simétrica que é usada para criptografar cadeias de caracteres e credenciais de conexões armazenadas. Você deve ter uma cópia de backup da chave simétrica caso altere a conta de serviço ou mova um banco de dados do servidor de relatório para outro computador.  
  
-   Configure a conta de execução autônoma. Essa conta é usada para conexões remotas durante operações agendadas ou quando as credenciais de usuário não estão disponíveis.  
  
-   Configure o email do servidor de relatório. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email do servidor de relatório que usa o protocolo SMTP para entregar relatórios ou notificação de processamento de relatórios a uma caixa de correio eletrônica. Você pode usar o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar qual servidor ou gateway SMTP na sua rede será usado para entrega de e-mail.  
  
 A ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não o ajuda a gerenciar o conteúdo do servidor de relatório, habilitar recursos adicionais ou conceder acesso ao servidor. A implantação completa exige que você também use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para habilitar recursos adicionais ou modificar valores padrão e o portal da Web para conceder acesso do usuário ao servidor.

##  <a name="bkmk_requirements"></a> Requisitos

O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager é específico da versão. O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalada com esta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser usado para configurar uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se você estiver executando versões mais antigas e mais novas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] lado a lado no mesmo computador, deverá usar o Gerenciador de Configurações do Reporting Services fornecido com cada versão para configurar cada instância.  

Para usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você deve ter o seguinte:

- Permissões de administrador de sistema local no computador que hospeda o servidor de relatório que você deseja configurar. Se você estiver configurando um computador remoto, deverá ter permissões de administrador de sistema locais nesse computador também.

- É necessário ter permissão para criar bancos de dados no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usado para hospedar o banco de dados do servidor de relatório.

- O serviço WMI (Instrumentação de Gerenciamento do Windows) deve ser ativado e executado em qualquer servidor de relatório que você estiver configurando. O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa o provedor WMI do servidor de relatório para se conectar a servidores de relatório locais e remotos. Se você estiver configurando um servidor de relatório remoto, o computador deverá conceder acesso WMI remoto. Para obter mais informações, consulte [Configurar um Servidor de Relatório para Administração Remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  

- Antes de conectar-se a e configurar uma instância remota do servidor de relatório, você deve habilitar as chamadas remotas à WMI (Instrumentação de Gerenciamento do Windows) para passar pelo o Firewall do Windows. Para obter mais informações, consulte [Configurar um Servidor de Relatório para Administração Remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

O Gerenciador de Configurações do Reporting Services é instalado automaticamente quando você instala o SQL Server Reporting Services.

##  <a name="bkmk_start_configuration_manager"></a> Para iniciar o Gerenciador de Configuração do Reporting Services

1.  Use a seguinte etapa que for apropriada para sua versão do Microsoft Windows:

    - Na tela inicial do Windows, digite **Relatórios** e selecione **Gerenciador de Configurações do Reporting Services** nos resultados da pesquisa.

    - Selecione **Iniciar**, aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]e aponte para **Ferramentas de Configuração**.

         Para configurar uma instância do servidor de relatório de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra a pasta do programa dessa versão. Por exemplo, aponte para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , em vez de [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] para abrir as ferramentas de configuração para os componentes de servidor do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .

         Selecione **Gerenciador de Configuração do Reporting Services**.

2. A caixa de diálogo **Conexão de Configuração do Reporting Services** será exibida, para que você possa selecionar a instância do servidor de relatório que deseja configurar. Selecione **Conectar**.

3. Em **Nome do Servidor**, especifique o nome do computador no qual a instância do servidor de relatório está instalada. O nome do computador local aparece por padrão, mas você pode digitar o nome de uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar-se a um servidor de relatório que esteja instalado em um computador remoto.

4. Se você especificar um computador remoto, selecione **Localizar** para estabelecer uma conexão.

5. Em **Report Server Emstance**, selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que deseja configurar. Somente instâncias de servidor de relatório para esta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparecem na lista. Você não pode configurar versões anteriores do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

6. Selecione **Conectar**.

## <a name="next-steps"></a>Próximas etapas

[Portal da Web](../../reporting-services/web-portal-ssrs-native-mode.md)   
[Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
[Configurar uma conexão de banco de dados do Servidor de Relatório](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)   
[Configurar e administrar um servidor de relatório](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
