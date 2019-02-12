---
title: Configurar o acesso ao Construtor de Relatórios | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, Report Builder
- Report Builder 1.0, configuring access
- configuring servers [Reporting Services]
ms.assetid: a79003d0-c905-4d4c-9560-93a7cc1e1dd4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 421c499b5135bc6022eafbc8d7fa6bf4456ca19a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020198"
---
# <a name="configure-report-builder-access"></a>Configurar o acesso ao Construtor de Relatórios
  O Construtor de Relatórios é uma ferramenta de criação de relatórios ad hoc instalada com um servidor de relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para o modo nativo ou o modo de integração no SharePoint.  
  
 O acesso ao Construtor de Relatórios depende dos seguintes fatores:  
  
-   As propriedades de servidor que determinam se o Construtor de Relatórios está disponível no servidor de relatório.  
  
-   As atribuições de função ou permissões que disponibilizam o Construtor de Relatórios para usuários individuais ou grupos.  
  
-   As configurações de autenticação que determinam se as credenciais de usuário podem ser transmitidas através do servidor de relatório ou se o acesso anônimo está configurado nos arquivos de aplicativo.  
  
 Para usar o Construtor de Relatórios, você deve ter um modelo de relatório publicado.  
  
## <a name="prerequisites"></a>Prerequisites  
 O Construtor de Relatórios não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 O computador cliente deve ter o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 instalado. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornece a infraestrutura para executar aplicativos [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] .  
  
 Você deve usar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 ou posterior.  
  
 O Construtor de Relatórios sempre é executado no modo de confiança total; você não pode configurá-lo para ser executado em confiança parcial. Nas versões anteriores, era possível executar o Construtor de Relatórios em confiança parcial, mas essa opção não é suportada no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores.  
  
## <a name="enabling-and-disabling-report-builder"></a>Habilitando e desabilitando o Construtor de Relatórios  
 O Construtor de Relatórios é habilitado por padrão. Os administradores de servidor de relatório têm a opção de desabilitar o recurso Construtor de Relatórios, definindo a propriedade de sistema do servidor de relatório `EnableReportDesignClientDownload` como `false`. A definição dessa propriedade desabilitará os downloads do Construtor de Relatórios para esse servidor de relatório.  
  
 Para definir propriedades de sistema do servidor de relatório, você pode usar o Management Studio ou script:  
  
-   Para usar o Management Studio, conecte-se ao servidor de relatório e use a página Propriedades Avançadas do Servidor para definir `EnableReportDesignClientDownload` como `false`. Para obter mais informações sobre como abrir essa página, consulte [Definir as propriedades do servidor de relatório &#40;Management Studio&#41;](../tools/set-report-server-properties-management-studio.md).  
  
-   Para ver um exemplo de script que define uma propriedade de servidor de relatório, consulte [Implantação de script e tarefas administrativas](../tools/script-deployment-and-administrative-tasks.md).  
  
## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>Atribuições de função que concedem o acesso ao Construtor de Relatórios em um servidor de relatório no modo nativo  
 Em um servidor de relatório no modo nativo, crie atribuições de função de usuário que incluem tarefas para usar o Construtor de Relatórios. Você deve ser Gerenciador de Conteúdo e Administrador de Sistema para criar ou modificar definições de função e atribuições de função em itens e no nível de site.  
  
 As instruções a seguir presumem que você está usando funções predefinidas. Se você tiver modificado as definições de função ou feito a atualização a partir do SQL Server 2000, verifique se as funções contêm as tarefas necessárias. Para obter mais informações sobre como criar atribuições de função, consulte [Conceder acesso ao usuário a um servidor de relatório &#40;Gerenciador de Relatórios&#41;](../security/grant-user-access-to-a-report-server.md).  
  
 Depois que você criar as atribuições de função, os usuários terão permissão para fazer o seguinte:  
  
-   Os usuários com as funções Usuário do Sistema e Navegador podem exibir os relatórios publicados do Construtor de Relatórios em um servidor de relatório, sem precisar iniciar o Construtor de Relatórios.  
  
-   Os usuários com as funções Usuário do Sistema e Construtor de Relatórios podem gerar modelos, iniciar o Construtor de Relatórios e criar relatórios, além de salvá-los no servidor de relatório.  
  
-   Os usuários com as funções Usuário do Sistema e Publicador podem publicar modelos do Designer de Modelo no servidor de relatório. Os modelos são usados como fontes de dados no Construtor de Relatórios.  
  
-   Os usuários com as funções Administrador do Sistema e Gerenciador de Conteúdo têm permissões completas para criar, exibir e gerenciar relatórios do Construtor de Relatórios.  
  
#### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>Para verificar se as tarefas necessárias estão nas definições de função  
  
1.  Inicie o Management Studio e conecte-se ao servidor de relatório.  
  
2.  Abra a pasta **Segurança** .  
  
3.  Abra a pasta **Funções do Sistema** .  
  
4.  Clique com o botão direito do mouse em **Administrador do Sistema**e selecione **Propriedades**.  
  
5.  Selecione **Executar definições de relatórios** e clique em **OK**.  
  
6.  Clique com o botão direito do mouse em **Usuário do Sistema**e selecione **Propriedades**.  
  
7.  Selecione **Executar definições de relatórios** e clique em **OK**.  
  
8.  Abra a pasta **Funções** .  
  
9. Clique com o botão direito do mouse em **Navegador**e selecione **Propriedades**.  
  
10. Selecione **Exibir modelos** e clique em **OK**.  
  
11. Clique com o botão direito do mouse em **Gerenciador de Conteúdo**e selecione **Propriedades**.  
  
12. Selecione **Exibir modelos**, **Gerenciar modelos**, **Relatórios de consumo**e clique em **OK**.  
  
13. Clique com o botão direito do mouse em **Publicador**e selecione **Propriedades**.  
  
14. Selecione **Gerenciar modelos** e clique em **OK**.  
  
15. Se não existir, crie a função do Construtor de Relatórios:  
  
    1.  Abra a pasta **Segurança** .  
  
    2.  Clique com o botão direito do mouse em **Funções**e selecione **Nova Função**.  
  
    3.  Em Nome, digite **Construtor de Relatórios**.  
  
    4.  Em Descrição, insira uma descrição para a função de modo que os usuários do Gerenciador de Relatórios saibam de que se trata a função.  
  
    5.  Adicione as seguintes tarefas: **Relatórios de consumo**, **exibir relatórios**, **exibir modelos**, **exibir recursos**, **exibir pastas**, e  **Gerenciar assinaturas individuais**s.  
  
    6.  Clique em **OK** para salvar a função.  
  
#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>Para criar atribuições de função que concedem acesso ao Construtor de Relatórios  
  
1.  Inicie o Gerenciador de Relatórios.  
  
2.  Clique em **Configurações de Site**.  
  
3.  Clique em **Segurança**.  
  
4.  Se uma atribuição de função já existir para o usuário ou grupo para o qual deseja configurar o acesso do Construtor de Relatórios, clique em **Editar**.  
  
     Caso contrário, clique em **Atribuição de Nova Função**. Em Grupo ou usuário, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.  
  
5.  Selecione **Usuário do Sistema**e clique em **OK**.  
  
6.  Clique em **Página inicial**.  
  
7.  Clique na guia **Configurações de Pasta** .  
  
8.  Clique na guia **Segurança** .  
  
9. Se uma atribuição de função já existir para o usuário ou grupo para o qual deseja configurar o acesso do Construtor de Relatórios, clique em **Editar**.  
  
     Caso contrário, clique em **Atribuição de Nova Função**. Em Grupo ou usuário, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.  
  
10. Selecione **Construtor de Relatórios**e clique em **Aplicar**.  
  
11. Repita o procedimento para criar ou modificar atribuições de função para usuários ou grupos adicionais.  
  
## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>Permissões que concedem acesso ao Construtor de Relatórios em um servidor de relatório no modo integrado do SharePoint  
 Em um servidor de relatório no modo integrado do SharePoint, o acesso ao Construtor de Relatórios é concedido aos usuários do SharePoint que têm os níveis de permissão Colaboração ou Controle Total.  
  
 Se você usar níveis de permissão personalizados, inclua Adicionar Itens e Editar Itens no nível de permissão. Para obter mais informações sobre o acesso ao Construtor de Relatórios por meio de níveis de permissão internos, consulte [Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório](../security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md). Para obter mais informações sobre requisitos de permissão para níveis de permissão personalizados, consulte [Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint](../security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="authentication-considerations-and-credential-reuse"></a>Considerações de autenticação e reutilização de credenciais  
 O Construtor de Relatórios usa a tecnologia ClickOnce para fazer download e instalar seus arquivos de aplicativo em um computador cliente. A tecnologia ClickOnce foi desenvolvida para a implantação unidirecional de aplicativos que coloca arquivos de programa em um computador cliente e executa o aplicativo como um processo separado com a identidade do usuário padrão. Como o Construtor de Relatórios deve se conectar novamente com o servidor de relatório para obter arquivos de aplicativo e dados do servidor de relatório, é importante entender como o ClickOnce define o contexto de segurança e faz solicitações para computadores remotos em cenários diferentes:  
  
-   O ClickOnce sempre é executado como um processo separado no computador cliente. A identidade de processo são as credenciais de usuário padrão do Windows. O ClickOnce não compartilha dados de sessão com o Internet Explorer nem obtém o contexto de segurança de usuário atual do Internet Explorer.  
  
-   O ClickOnce envia solicitações que especificam a segurança integrada do Windows no cabeçalho de autenticação. Se um servidor estiver configurado para um tipo de autenticação diferente, ele não atenderá às solicitações do ClickOnce e exibirá um erro de autenticação. Para resolver esse problema, configure um servidor para a segurança integrada do Windows ou habilite o acesso Anônimo para eliminar a verificação de autenticação.  
  
-   O Construtor de Relatórios abre sua própria conexão com um servidor de relatório. Se não estiver usando a segurança integrada do Windows com logon único, os usuários devem digitar novamente suas credenciais para conectar o Construtor de Relatórios com o servidor de relatório.  
  
 A tabela a seguir descreve os tipos de autenticação suportados pelo servidor de relatório e informa se alguma configuração adicional é necessária para acessar o Construtor de Relatórios.  
  
|Tipo de autenticação do servidor de relatório|Como o Construtor de Relatórios e o aplicativo de inicialização ClickOnce respondem|  
|---------------------------------------|--------------------------------------------------------------------|  
|Negotiate (padrão)<br /><br /> NTLM (padrão)|Na segurança integrada do Windows, as solicitações autenticadas do ClickOnce e do Construtor de Relatórios serão bem-sucedidas se o cliente e o servidor estiverem implantados no mesmo domínio, se o usuário estiver conectado no computador cliente usando uma conta de domínio com permissão para acessar o Construtor de Relatórios e se o servidor de relatório estiver configurado para a Autenticação do Windows.<br /><br /> As solicitações são bem-sucedidas porque o ClickOnce e a conexão do navegador com o servidor de relatório têm a mesma identidade de usuário.<br /><br /> As solicitações falharão se o usuário tiver aberto o Internet Explorer com o comando Executar como e tiver especificado credenciais não padrão. Se a sessão de usuário no servidor de relatório for estabelecida por meio de uma conta específica e o ClickOnce for executado em uma conta diferente, o servidor de relatório negará o acesso aos arquivos.|  
|Kerberos|O Internet Explorer, que é necessário para usar o Construtor de Relatórios, não dá suporte para o Kerberos diretamente.|  
|Autenticação Básica|O ClickOnce não dá suporte à autenticação básica. Ele não fará solicitações que especificam a autenticação básica no cabeçalho de autenticação. Não transmitirá credenciais nem solicitará que o usuário as forneça. Você pode resolver esses problemas habilitando o acesso Anônimo aos arquivos de aplicativo do Construtor de Relatórios.<br /><br /> As solicitações serão bem-sucedidas se o acesso Anônimo for habilitado para os arquivos de aplicativo do Construtor de Relatórios porque o servidor de relatórios ignora o cabeçalho de autenticação. Para obter mais informações sobre como habilitar o acesso Anônimo ao Construtor de Relatórios, consulte [Configurar a autenticação Básica no servidor de relatório](../security/configure-basic-authentication-on-the-report-server.md).<br /><br /> Depois que o ClickOnce recupera os arquivos de aplicativo, o Construtor de Relatórios abre uma conexão separada com um servidor de relatório. Os usuários devem digitar novamente suas credenciais para conectar o Construtor de Relatórios ao servidor de relatório. O Construtor de Relatórios não coleta credenciais a partir do Internet Explorer ou do ClickOnce.<br /><br /> As solicitações falharão se o servidor de relatório estiver configurado para a autenticação básica e você não tiver habilitado o acesso Anônimo aos arquivos de programa do Construtor de Relatórios. A solicitação falha porque o ClickOnce especifica a segurança integrada do Windows em suas solicitações. Se o servidor de relatório for configurado para a autenticação básica, a solicitação será rejeitada porque especifica um pacote de segurança inválido e não tem as credenciais esperadas pelo servidor de relatório.<br /><br /> Além disso, se o servidor de relatório estiver configurado para usar o modo integrado do SharePoint e o site do SharePoint usar a autenticação Básica, os usuários encontrarão um erro 401 quando tentarem usar o ClickOnce para instalar o Construtor de Relatórios em seus computadores cliente. Isso acontece porque o SharePoint usa um cookie para manter um usuário autenticado enquanto durar a sessão, mas o ClickOnce não dá suporte ao cookie. Quando um usuário iniciar um aplicativo ClickOnce, como o Construtor de Relatórios, o aplicativo não passará o cookie para o SharePoint e, portanto, o SharePoint negará o acesso e retornará um erro 401.<br /><br /> Você pode contornar esse problema tentando uma das seguintes opções:<br /><br /> Selecione o **Lembrar minha senha** opção ao fornecer suas credenciais de usuário.<br /><br /> Habilite o acesso Anônimo à coleção de sites do SharePoint.<br /><br /> Configure o ambiente de forma que o usuário não forneça credenciais. Por exemplo, em um ambiente de Intranet, você poderá configurar o servidor do SharePoint para pertencer a um Grupo de Trabalho e, em seguida, criar contas de usuário no computador local.|  
|Personalizar|Ao configurar um servidor de relatório para usar a autenticação personalizada, o acesso Anônimo é habilitado no servidor de relatório e as solicitações são aceitas sem nenhuma verificação de autenticação.<br /><br /> Depois que o ClickOnce recupera os arquivos de aplicativo, o Construtor de Relatórios abre uma conexão separada com um servidor de relatório. Os usuários devem digitar novamente suas credenciais para conectar o Construtor de Relatórios ao servidor de relatório. O Construtor de Relatórios não coleta credenciais a partir do Internet Explorer ou do ClickOnce.|  
  
## <a name="see-also"></a>Consulte também  
 [Autenticação com o servidor de relatório](../security/authentication-with-the-report-server.md)   
 [Planning for Reporting Services e o suporte a navegador Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [Iniciar o construtor de relatórios &#40;construtor de relatórios&#41;](../report-builder/start-report-builder.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../tools/connect-to-a-report-server-in-management-studio.md)   
 [Propriedades do sistema do servidor de relatório](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)  
  
  
