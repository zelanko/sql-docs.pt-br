---
title: Configurar a conta de serviço do servidor de relatório (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f880c623-67c8-4167-b98b-ace17e800faa
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f13a9693615fd55d1cd9fed60398ab78374963e0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282762"
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>Configurar a conta de serviço do servidor de relatório (Gerenciador de configurações SSRS)
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é implementado com um único serviço que contém um serviço Web do Servidor de Relatório, um Gerenciador de Relatórios e um aplicativo de processamento em segundo plano usado para processamento agendado de relatórios e entrega de assinaturas. Este tópico explica como uma conta de serviço é configurada inicialmente e como modificar a conta ou a senha usando a ferramenta Configuração do Reporting Services.  
  
## <a name="initial-configuration"></a>Configuração inicial  
 A conta de serviço do Servidor de Relatório é definida durante a Instalação. Você pode executar o serviço sob uma conta de usuário de domínio ou uma conta interna, como `NetworkService` conta. Não há nenhuma conta padrão; qualquer conta que você especificar o [configuração do servidor — contas de serviço](../../sql-server/install/server-configuration-service-accounts.md) página do Assistente de instalação se torna a conta inicial do serviço servidor de relatório.  
  
> [!IMPORTANT]  
>  Embora o serviço Web do servidor de relatório e Gerenciador de relatórios sejam [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] aplicativos, eles não são executados sob o [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] conta. A única arquitetura de serviço executa ambos os aplicativos ASP.NET na mesma identidade de processo do Servidor de Relatório. Essa é uma alteração importante de versões anteriores em que tanto o serviço Web Servidor de Relatórios quanto o Gerenciador de Relatórios eram executados na identidade do processo de trabalho do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] especificada no IIS.  
  
## <a name="changing-the-service-account"></a>Alterando a conta de serviço  
 Para exibir e reconfigurar as informações da conta de serviço, sempre use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. As informações sobre identidade de serviço são armazenadas internamente em vários locais. O uso da ferramenta garante que todas as referências sejam adequadamente atualizadas sempre que você alterar a conta ou a senha. A ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] executa as seguintes etapas adicionais para garantir que o servidor de relatório permaneça disponível:  
  
-   Adiciona automaticamente a nova conta para o grupo de servidor de relatório criado no computador local. Esse grupo é especificado nas ACLs (listas de controle de acesso) que protegem os arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Atualiza automaticamente as permissões de logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usada para hospedar o banco de dados do servidor de relatório. A nova conta será adicionada ao **RSExecRole**.  
  
     O logon do banco de dados da conta antiga não é removido automaticamente. Lembre-se de remover contas que não estejam mais sendo usadas. Para obter mais informações, consulte [Administrar um banco de dados de servidor de relatório &#40;modo nativo do SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md) nos Manuais Online do SQL Server.  
  
     A concessão de permissões do banco de dados para a nova conta de serviço acontece apenas se você tiver configurado a conexão do banco de dados do servidor de relatório para usar a conta de serviço. Se tiver configurado a conexão do banco de dados do servidor de relatório para usar uma conta de usuário do domínio ou um logon do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , as informações sobre a conexão não terão sido afetadas pela atualização da conta de serviço.  
  
-   Atualiza automaticamente a chave de criptografia para incluir as informações de perfil da conta nova.  
  
    > [!NOTE]  
    >  Se o servidor de relatório fizer parte da implantação em expansão, somente o servidor de relatório que você está atualizando será afetado. As chaves de criptografia para outros servidores de relatório na implantação não são afetadas pela alteração da conta de serviço.  
  
 Para obter instruções sobre como definir a conta, consulte [configurar uma conta de serviço &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md).  
  
## <a name="choosing-an-account"></a>Escolhendo uma conta  
 Você pode configurar o serviço Servidor de Relatório para ser executado em qualquer um destes tipos de conta:  
  
-   Conta de usuário menos privilegiada do Windows  
  
-   NetworkService  
  
-   LocalSystem  
  
-   LocalService  
  
 Não há nenhum tipo de conta que possa ser considerado o melhor. Cada conta tem vantagens e desvantagens que devem ser consideradas. Se você estiver implantando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um servidor de produção, as práticas recomendadas sugerem que você configure o serviço seja executado em uma conta de usuário de domínio para que você pode evitar danos extensivos caso uma conta compartilhada seja comprometida por um usuário mal-intencionado. Isso também facilita a auditoria das atividades de logon dessa conta. Uma desvantagem usando uma conta de usuário do Windows é que, se você estiver implantando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma rede que usa autenticação Kerberos, você deve registrar o serviço com a conta de usuário. Para obter mais informações, consulte [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](../report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
 Os links e as diretrizes a seguir irão ajudá-lo a decidir qual a melhor opção para sua implantação.  
  
-   [Conta de serviço &#40;modo nativo do SSRS&#41;](../../sql-server/install/service-account-ssrs-native-mode.md).  
  
-   [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) nos Manuais Online do SQL Server.  
  
-   [The Services and Service Accounts Security Planning Guide](http://go.microsoft.com/fwlink/?LinkId=69155) (O Guia de planejamento de segurança de serviços e contas de serviço) no MSDN.  
  
## <a name="updating-an-expired-password"></a>Atualizando uma senha expirada  
 Se o serviço Servidor de Relatório for executado em uma conta de domínio e a senha expirar antes de você atualizá-la na ferramenta Configuração do Reporting Services, o serviço não será iniciado até que seja especificada uma nova senha. Se o serviço não puder ser iniciado, não será possível usar a ferramenta Configuração do Reporting Services para se conectar ao servido e atualizar a conta. Nesse caso, você deve usar uma combinação de ferramentas para fazer com que o servidor fique novamente online.  
  
 Para redefinir a senha faça o seguinte:  
  
1.  Sobre o **iniciar** , aponte para **painel de controle**, aponte para **ferramentas do administrador**e clique em **serviços**.  
  
2.  Clique com botão direito **SQL Server Reporting Services**, selecione **propriedades**.  
  
3.  Clique em **fazer logon**e digite a nova senha.  
  
4.  Depois de atualizar a senha, inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e atualize a senha na página Conta de Serviço. Essa etapa adicional é necessária para atualizar as informações da conta que são armazenadas internamente pelo servidor de relatório.  
  
 Se a senha da conta de serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] expirar, ocorrerá o erro `rsReportServerDatabaseUnavailable` quando você tentar se conectar ao servidor de relatório. A redefinição da senha resolve esse erro.  
  
## <a name="configuring-the-report-server-service-for-a-sharepoint-integrated-report-server"></a>Configurando o serviço Servidor de Relatório para um servidor de relatório integrado do SharePoint  
 Se estiver executando um servidor de relatório no modo integrado do SharePoint, você deverá atualizar as informações da conta de serviço armazenadas no banco de dados de configuração do SharePoint, caso ocorra alguma das seguintes condições:  
  
-   Modificando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] conta (por exemplo, alternando de serviço de rede para uma conta de usuário de domínio) de serviço.  
  
-   Extensão de um farm do SharePoint para incluir um aplicativo adicional da Web do SharePoint. Se o farm do servidor for configurado para integração do servidor de relatório e o aplicativo adicionado recentemente for configurado para ser executado em uma conta de usuário diferente dos outros aplicativos no farm, você deverá atualizar as informações de acesso ao banco de dados.  
  
 Depois de redefinir as informações de acesso ao banco de dados, você deve reiniciar o serviço [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] para garantir que a conexão antiga não seja mais usada.  
  
1.  Na **ferramentas administrativas**, clique em **Administração Central do SharePoint 2010**.  
  
2.  Clique em **gerenciamento de aplicativos**.  
  
3.  Na seção Reporting Services, clique em **conceder acesso ao banco de dados**.  
  
4.  Clique em **OK**. A caixa de diálogo Inserir Credenciais é exibida.  
  
5.  Insira as credenciais de um usuário que seja membro do grupo Administrador local no computador que hospeda o servidor de relatório. As credenciais serão usadas para uma conexão única com o computador do servidor de relatório a fim de recuperar informações da conta de serviço. O logon do banco de dados criado para cada conta de serviço será atualizado nos bancos de dados do SharePoint.  
  
6.  Para reiniciar o serviço, clique em **operações**.  
  
7.  Na topologia e serviços, clique em **os serviços no servidor**.  
  
8.  Para o aplicativo Web do Windows SharePoint Services, clique em **parar**.  
  
9. Aguarde até o serviço parar.  
  
10. Clique em **iniciar**.  
  
> [!NOTE]  
>  Os produtos e tecnologias do SharePoint exigem contas de domínio para a configuração de serviço, como o modo do SharePoint do Reporting Services.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar uma conta de serviço &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Conta de serviço &#40;modo nativo do SSRS&#41;](../../sql-server/install/service-account-ssrs-native-mode.md)   
 [Configurar as URLs de servidor de relatório &#40;Configuration Manager do SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
